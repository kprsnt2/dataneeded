# JobAgents: a job pipeline that refuses to fabricate

I built JobAgents to solve my own job search, and the first thing I had to admit
was that the problem is not browsing.

Every job board is optimised for browsing: infinite scroll, saved searches, an
email digest. Browsing is a fine interface when you have three roles to look at
and a bad one when you have seven thousand. The actual work is sourcing —
finding every posting that matches a defined target, scoring them consistently,
deduplicating the ones that appear on five boards at once, and only then
spending effort on the handful worth an application. That is a data pipeline
problem wearing a consumer-product costume.

So JobAgents is a pipeline. It sources from ATS APIs and aggregators, scores
every job deterministically, tailors a resume for the top matches, drafts
outreach, and validates those drafts against code invariants. It runs unattended
on a schedule. And it will not send anything, ever, by construction.

This post is about the decisions that mattered, the guard that turned out to be
the real deliverable, and the parts that are still broken.

---

## The decision that mattered: ATS-first, not social-first

The original plan had social media as the primary source. That was wrong, and
the probe said so before a line of the adapter was written.

Greenhouse, Ashby, and Lever expose public JSON endpoints with structured
salary, location, seniority, and full descriptions. LinkedIn, X, and Indeed are
login-walled, ToS-restricted, and ban-prone. The first run made the asymmetry
concrete: the three ATS boards carried 7,151 of 7,287 jobs, and the public
aggregator APIs added 136 more (`README.md`).

| Source class | Access | Structured fields | First-run yield |
|---|---|---|---|
| Greenhouse / Ashby / Lever | Public JSON | Salary, location, seniority, description | 7,151 |
| RemoteOK / Remotive / HN | Public JSON APIs | Location, tags, description | 136 |
| LinkedIn / X / Indeed | Login-walled, ban-prone | Cards, inconsistent | Secondary signal |

Two things I learned from probing rather than assuming, both of which changed
the adapter:

1. **LinkedIn guest search has no usable JSON-LD.** The
   `<script type="application/ld+json">` path yields roughly one block. The real
   data lives in `<li>` cards carrying `data-entity-urn="urn:li:jobPosting:<id>"`,
   and `jobagents/linkedin.py` parses those instead.
2. **Adding `&f_TPR=` collapses the result set to near-zero.** The recency
   filter has to be applied *after* parsing, in the scorer, not via the URL.

Social did earn a place, but not the one it was originally assigned. LinkedIn
surfaced India roles — Accenture, Optum, Qualys, Albertsons, UST — that the ATS
boards missed entirely. And the whole "X and Indeed need a logged-in browser"
conclusion in my first plan turned out to be wrong: an early probe used raw
`urllib`, got a 403, and drew a conclusion that a 403 does not support. Routing
those platforms through a search index instead returns real Indeed job URLs and
real X hiring posts with no authentication at all. Social sourcing became
search-index-based, which is strictly better than scraping: no session, no
login, no ban risk.

The general lesson is narrower than "probe your environment." It is that a 403
on one access path tells you nothing about a different access path to the same
data, and a plan written before the probe will encode the wrong conclusion
confidently.

---

## Deterministic matching as a cost gate

The matching service is the load-bearing cost decision. It runs on every job for
free, so only the top-N ever reach a model.

`jobagents/matching.py` is arithmetic and string matching — five weighted
components, no model call anywhere:

```python
# jobagents/matching.py:7-12
#     title_match     0.30   fuzzy title similarity to track titles
#     keyword_overlap 0.30   must-have keywords present in the JD
#     seniority_fit   0.15   mid-senior, penalise intern/manager/exec
#     location_fit    0.15   India or remote-global or visa-sponsoring
#     recency         0.10   newer postings score higher
```

The current database holds **22,647 match scores** across three tracks. The
model calls required to produce them: **zero**.

| Funnel stage | Count |
|---|---|
| Sourced | 7,549 |
| Scores computed | 22,647 |
| Above threshold (score ≥ 65) | 274 |
| Resumes generated | 1 |
| Drafts written | 10 |

*Snapshot: `job.kprsnt.in`, 2026-10-05 18:58:59 UTC.*

The ratio is the point. 22,647 scores cost nothing; 274 candidates are the only
ones eligible to consume a model call. If I had asked a model to judge every
posting — the obvious design — the cost would scale with sourcing volume, and
sourcing volume is the one thing a pipeline like this is supposed to maximise.

The source mix that produced those 7,549 rows shows where the volume actually
comes from:

| Source | Jobs | Share |
|---|---|---|
| greenhouse | 4,364 | 58% |
| ashby | 2,396 | 32% |
| lever | 399 | 5% |
| linkedin | 241 | 3% |
| remoteok | 99 | 1% |
| hn / remotive / search:* | 50 | <1% |

Ten sources, and the top two carry 90%. The long tail is not useless — the
search-index sources are what reach X and Indeed without a session — but the
volume argument for ATS-first is not close.

The score distribution shows the gate working, and also shows it is set loosely:

| Band | Count |
|---|---|
| 90–100 | 1 |
| 80–89 | 11 |
| 70–79 | 103 |
| 60–69 | 454 |
| 50–59 | 1,621 |
| 0–49 | 20,457 |

Almost everything lands below 50. A hard threshold at 65 admits 274 — and
because the default `--tailor-limit` is 10, the queue grows faster than the
machine drains it. That is not a working configuration, and it is the first
thing the post-pipeline playbook tells me to fix: raise the bar or raise the
limit, but do not leave 274 queued against a limit of 10 and assume the machine
is working the list.

### Two bugs in the scorer worth naming

Both were found by reading real output, not by testing.

**Substring keyword matching.** `bias` matched inside `unbiased`, and short
tokens like `ai` and `sql` matched inside unrelated words. Fixed with whole-word
regex boundaries.

**Track weight scaled the score.** The AI Safety track carried a weight of 0.6,
which mathematically capped it at roughly 60 against a 65 threshold — so it
found **zero** candidates despite having strong matches. The weight was
expressing the wrong thing. It now applies a mild confidence damp rather than
scaling the score, and expresses *outreach priority* instead. Candidates went
from **0 to 13** (`PLAN.md` §12).

That second one is the more instructive failure. A track configured to be
deliberately lower-priority was silently reduced to a track that returned
nothing, and nothing in the run reported an error. It looked exactly like a
track with no matches.

---

## Two-layer dedupe

The same role advertised on Greenhouse, LinkedIn, and RemoteOK is one
opportunity, not three. But each posting is also a real record with real
provenance, and I did not want to throw that away.

So dedupe runs in two layers (`jobagents/store.py:230-273`):

```sql
-- Layer 1: the same posting re-fetched from the same source
UNIQUE(source, external_id)
```

```python
# Layer 2: jobagents/store.py:153-174
def make_dedupe_key(company: str, title: str, location: str | None = None) -> str:
    """...Intentionally ignores location: the same role advertised in several
    cities is still one opportunity for outreach purposes."""
    ...
    return f"{comp}|{ttl}"
```

Layer 2 only *links*; it never deletes. Every row keeps its source, URL, and
`external_id`, so provenance survives the merge.

**Location is deliberately excluded from the key.** One role posted in five
cities is one outreach target. This is not a detail — it is the difference
between a pipeline that sends one email and a pipeline that sends five
near-identical ones to the same company. Outreach later reproduced exactly that
bug when it drafted for two `jobs` rows representing one Affirm opening
advertised in Spain and Poland, producing four near-identical applications. The
fix was to collapse on `make_dedupe_key` before spending a model call
(`jobagents/agents/outreach.py:545-562`), which is what the key was already
built to express.

Current totals: **5,801 distinct roles** from **7,549 jobs**, with **1,748
duplicates merged**.

The key also strips company suffixes (`inc`, `ltd`, `gmbh`, `technologies`, …)
and leading seniority noise (`senior`, `lead`, `staff`, `principal`), so
"Senior Python Developer" and "Python Developer" at the same company collapse.

---

## The anti-fabrication guard is the actual deliverable

I expected the guard to be defensive plumbing. It turned out to be the most
valuable thing in the repository, because it caught a real model output that
would otherwise have shipped.

`jobagents/tailor.py` generates a job-specific resume and then validates it
against `config/profile.md` **in code, before writing it to disk**. A resume
that fails validation is never persisted (`jobagents/tailor.py:389-398`). The
rules are enumerated in the module docstring and enforced in
`validate_resume()` (`jobagents/tailor.py:106-185`): every number must trace to
the profile's Verified Metrics table, no employer or title absent from the
profile, no seniority inflation, no disclosure-unsafe terms, word budget
respected.

### What it caught

Two real model outputs were rejected during testing. One invented the figure
`120`. The other was worse: it **attributed BugAgents, AI Eco, Awakening, and
BrandXY to Black Piano as employment**. Those are my independent projects. Black
Piano is my employer. The model merged them into an employment history that does
not exist.

The prompt forbade exactly this. The prompt said, in capitals, that the
candidate has exactly two employers and that everything else is independent
project work. The model did it anyway.

A prompt-only rule would have shipped a fabricated resume. So attribution became
a checker — `_check_attribution()` (`jobagents/tailor.py:196-242`) walks the
Markdown, tracks the current employer section, and rejects any project name
appearing as a bullet inside an employer's block:

```python
# jobagents/tailor.py:232-240
# Bullets inside a real employer block must not claim project work
if current_is_real and re.match(r"^\s*[-*]\s+", line):
    low = line.lower()
    for proj in _PROJECT_NAMES:
        if proj in low:
            problems.append(
                f"independent project '{proj}' attributed to employer "
                f"'{current_employer}' — must be under a projects heading")
```

The guard also catches seeded fabrications — eight of eight — across the
violation classes: a fabricated employer name, an invented performance figure, a
seniority title the candidate does not hold, a disclosure-unsafe vendor name, an
unverifiable bounty-status claim, a team-management claim, and a
business-metric claim (`PLAN.md` §13).

### Prompt rules are not guards

This is the transferable lesson, and it generalises past resumes.

A prompt rule is a *request*. It is evaluated by the same model that is
generating the content, in the same pass, under the same pressure to produce
something fluent and complete. When the instruction conflicts with what the
model finds plausible, the instruction loses — not always, but often enough that
you cannot build on it. And when it loses, it loses **silently**. There is no
exception, no error, no log line. There is just a confident document with a
false claim in it.

A guard is different in kind. It runs after generation, it runs in code, it has
no opinion about plausibility, and it fails loudly. The model is untrusted input
to a validator, not a collaborator in a review.

The practical test I now apply: **if the rule is not enforced by something that
can reject the output, it is not a rule — it is a suggestion.** A rule that
exists only in a prompt should be labelled as such in your own head, because
that is what it is.

The honest limitation: the guard catches *structural* violations — a named
employer, an uncited figure, a withheld term, a seniority claim. A confidently
stated false metric that is *shaped* like a real one still passes. The profile
is the ground truth, but no code here diffs generated prose against the metrics
table claim by claim. That gap is real and it is not closed.

---

## The no-send invariant

The pipeline drafts outreach. It does not send it, and it cannot be made to.

This is structural, not a convention, and it is enforced three ways.

**No transmission library is imported.** The module's complete import list is
`__future__`, `json`, `re`, `sys`, `pathlib`, `typing`, plus the project's own
config, models, and store. There is no `smtplib`, no HTTP client, no browser
automation. Nothing to send *with*.

**The module audits its own source at runtime.**
`assert_no_send_path()` (`jobagents/agents/outreach.py:446-459`) reads its own
file, strips out the guard's own pattern table and function body, and returns
any send-capable construct it finds. An empty list is the invariant, and
`run_drafts` raises before doing anything else if it is violated
(`jobagents/agents/outreach.py:509-513`):

```python
# jobagents/agents/outreach.py:439-443
_SEND_PATH_PATTERNS: tuple[str, ...] = (
    "smtplib", "sendmail", "send_message(", "requests.post", "urlopen",
    "http.client", "httpx", "websocket", "selenium", "playwright",
    "pyautogui", "webbrowser",
)
```

This was verified in both directions: on the real module it returns `[]`, and on
a copy with `import smtplib` injected, the guard fires. The second half is the
part that matters — a check that has never failed is not evidence of anything.

**The send path does not exist in the API.** `drafts.sent_at` exists as a column
(`jobagents/store.py:78`) and is never written by any code in the repository.
The dashboard's draft endpoint accepts exactly two actions, and
`{"action":"send"}` returns HTTP 400 (`jobagents/web.py:420-424`):

```python
def update_draft(store: Store, draft_id: int, action: str) -> dict[str, Any]:
    """Approve or reject a draft. Never sends anything."""
    if action not in ("approve", "reject"):
        return {"ok": False, "error": f"unknown action {action!r}; "
                                      "expected 'approve' or 'reject'"}
```

The dashboard payload even hard-codes `"send_enabled": False`
(`jobagents/web.py:414`) so the UI cannot drift into offering a send button.

Why be this rigid? Because LinkedIn and X automation-detection bans are real and
account-ending. The draft-only invariant is the entire reason running this
pipeline is safe. Approval is a human decision; sending is a human action. That
is the boundary, and it is the one part of the system I will not "fix."

---

## Review as code invariants, not LLM-grading-LLM

The obvious design for the review stage is to ask a strong model "is this draft
good?" It does not work, and the failure is specific: **an LLM grading an LLM
rubber-stamps.**

A model judging text that another instance of itself produced in a plausible
register says yes, because the text *reads* correct. And a reviewer that returns
`pass` for everything is worse than no reviewer at all, because it manufactures
confidence in a verdict nobody verified.

So the review splits the work by what each side is actually good at
(`jobagents/agents/review.py`):

| Question | Who answers | Why |
|---|---|---|
| Does this name an employer not in `profile.md`? | Code | Set membership. Exact. |
| Does it leak a withheld vendor or asset term? | Code | Regex. Exact. |
| Is it 80–250 words / ≤300 chars? | Code | Arithmetic. Exact. |
| Is it a near-copy of a draft for another job? | Code | Token overlap. Reproducible. |
| Did one company get spammed? | Code | Counting. Exact. |
| *Is the tone right for cold outreach?* | **Model** | Genuine judgment. |

The model never overrides a code verdict. It is consulted only for a draft that
is clean on every hard check but ambiguous, and its answer is recorded as an
advisory in `checks_json`, never as a pass that erases a violation.

The escalation is gated twice for a reason. Escalating every clean draft would
make the model the decider again, which is the exact failure mode the module
exists to prevent. `escalated 0` on a healthy run is the correct outcome, not a
bug.

The checks are validated by **falsification**, not spot-checking:
`scripts/test_review_checks.py` deliberately violates every invariant and
asserts each one fires. Result: **0 failures**. A checker that only ever returns
`pass` is worthless, so proving the opposite is the only useful test.

### Two design bugs the tests caught

**The rate limit was unsatisfiable.** It counted draft *rows* per company, capped
at 2. But one application writes two rows — an email and a LinkedIn DM — so any
company that received even a single application was permanently in violation.
Fixed to count distinct **roles**, which is what "don't spam one recruiter"
actually means.

**The overclaim check flagged honest drafts.** It matched the bare noun
`revenue` anywhere, so every application to *"Analytics Engineer II, Full Stack
(Revenue Analytics)"* failed, as did the legitimate phrase "revenue data
modeling." A check that fails honest drafts trains the operator to ignore the
verdict, which is worse than having no check. Fixed to require a *claim
construction*: a possessive, a quantity, or a generated-value verb.

That second bug is the one I keep coming back to. The check was technically
correct — the word was present — and completely useless, because it fired on the
job title of a legitimate target. Precision failures in guards do not produce
false confidence; they produce *ignored* guards, which is the same outcome with
more steps.

---

## The honest gap: the funnel measures the top precisely and the bottom not at all

Here is what the pipeline actually knows.

| Stage | Automated? | Evidence |
|---|---|---|
| Source jobs | Yes, unattended, 09:00 IST | `scripts/run_daily.ps1` |
| Score / match | Yes, deterministic, zero model calls | `jobagents/matching.py` |
| Tailor resume | Yes, with code-enforced guard | `jobagents/tailor.py` |
| Draft outreach | Yes, draft-only | `jobagents/agents/outreach.py` |
| Review drafts | Yes, 11 code invariants | `jobagents/agents/review.py` |
| **Approve** | **No — me** | `POST /api/drafts/<id>` `{"action":"approve"}` |
| **Send** | **No — me, by hand** | `drafts.sent_at` is never written |
| **Track the outcome** | **Nothing exists** | — |

The `applications` table exists in the schema
(`jobagents/store.py:93-100`) and **no stage ever inserts into it**. A
full-tree grep for `applications` / `applied_at` finds only the schema and the
plan's own diagram. The dashboard exposes `GET /api/jobs` and `GET /api/jobs/<id>`
and no write endpoint for jobs at all — so the plan's claim that the Jobs tab can
"mark applied/rejected" is a doc-versus-code gap, not a feature.

The consequence is that the funnel ends at **Approved**. There is no "Sent"
stage and no "Replied" stage, because the system has no idea either of those
happened. **274 matches above threshold, 1 resume generated, 10 drafts written,
0 approved.** The queue is full and untouched.

So the machine can run perfectly forever and I would learn nothing about whether
any of it works. I cannot tell whether 65 is the right threshold, whether the
email or the LinkedIn DM converts, or whether tailoring helps at all. Every
application sent without recording it is an experiment thrown away.

The asymmetry is worth stating plainly: **the top of the funnel is measured to
the unit, and the bottom of it is not measured at all.** The pipeline knows
exactly how many postings it merged and how many scores it computed, and it does
not know whether a single message was ever answered. Building the precise half
was the easy half.

The fix is small, because the schema is already there — a `POST /api/applications`
route, an "Applied" button on the review card, and `Sent` / `Replied` stages in
the funnel. It is ranked first in the post-build playbook for a reason: every
other improvement compounds on a number I cannot currently see.

### Other limitations, stated plainly

- **Salary coverage is 21%** (1,557 of 7,549). ATS boards publish salary far more
  often than aggregators, so coverage is a function of source mix, not of the
  market.
- **Freshness skews old.** Only 188 jobs (2%) are from the last 24 hours; 2,640
  (35%) are older than 30 days. Postings stay open, but a stale posting is a
  worse bet.
- **The reviewer cannot detect a well-written fabrication.** It catches
  structural violations. A confidently-stated false metric shaped like a real one
  passes.
- **Duplicate detection is lexical.** Two drafts saying the same thing in
  different words score low on Jaccard and both pass. It catches template reuse,
  which is the common failure, not paraphrase.
- **The rate limit is per run, not per company over time.** Running outreach
  twice with a cleared `drafts` table can exceed the cap in aggregate.
- **The dashboard has no auth and binds to loopback only.** Anyone who can reach
  the port has full control, including config writes. It is a local tool and it
  must stay one.
- **`check_personalization` is a soft signal, not a hard check.** Keyword
  matching is substring-based, so a draft that paraphrases "data modeling" as
  "data models" is falsely flagged. Promoting it to hard would fail honest drafts
  — the same precision trap as the `revenue` bug.

---

## What I would tell someone building this

Three things transferred, and none of them are about job searching.

**Put the cost gate before the model, not around it.** Deterministic work is
free and model work is not, so the ordering decision — score everything, generate
for the top-N — is the architecture. Retrofitting a gate onto a system that
already calls a model per item is much harder than building the gate first.

**Write the guard before you trust the prompt.** The attribution checker exists
because a model ignored an explicit, capitalised instruction. If a rule matters,
something must be able to reject the output. The prompt can still carry the rule;
it just cannot be the enforcement.

**Falsify your checks, do not spot-check them.** Both review bugs and the
unsatisfiable rate limit were found by deliberately violating every invariant and
confirming the verdict flipped. A guard that has never failed is untested, and
a guard that fails honest work gets ignored — which is the same as not having it.

The pipeline is live at [job.kprsnt.in](https://job.kprsnt.in). It still will not
send anything, and it still cannot tell me what happened after I did.
