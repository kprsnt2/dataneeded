# Phase 4 & 5 — Outreach and Review

Two agents, one rule: **nothing is ever sent, and nothing is believed without a
deterministic check.**

- **Phase 4 — `jobagents/agents/outreach.py`** writes cold-email and LinkedIn-DM
  drafts for the top-scoring matches.
- **Phase 5 — `jobagents/agents/review.py`** grades those drafts with code
  invariants first, and calls a model only for the residual judgment call.

```bash
python -m jobagents outreach --limit 10        # generate drafts (never sends)
python -m jobagents review                     # code checks, then model
python -m jobagents review --no-model          # code checks only
```

---

## 1. Why the review is code-first

The obvious design — ask a strong model "is this draft good?" — does not work,
and the failure is specific: **an LLM grading an LLM rubber-stamps.** A model
judging text that another instance of itself produced in a plausible register
says yes, because the text *reads* correct. A reviewer that returns `pass` for
everything is worse than no reviewer, because it manufactures confidence in a
verdict nobody verified.

So Phase 5 splits the work by what each side is actually good at:

| Question | Who answers | Why |
|---|---|---|
| Does this name an employer not in `profile.md`? | Code | Set membership. Exact. |
| Does it leak a withheld vendor/asset term? | Code | Regex. Exact. |
| Is it 80–250 words / ≤300 chars? | Code | Arithmetic. Exact. |
| Is it a near-copy of a draft for another job? | Code | Token overlap. Reproducible. |
| Did one company get spammed? | Code | Counting. Exact. |
| *Is the tone right for cold outreach?* | **Model** | Genuine judgment. |

The model never overrides a code verdict. It is only consulted for a draft that
is **clean on every hard check but ambiguous** — and its answer is recorded as
an advisory in `checks_json`, never as a pass that erases a violation.

This is also why the escalation is *gated twice*. Escalating every clean draft
would make the model the decider again, which is the failure mode this module
exists to avoid. `escalated 0` on a healthy run is the correct outcome, not a
bug.

---

## 2. The draft-only guarantee

`outreach.py` cannot send anything. This is structural, not a convention:

**No transmission library is imported.** The complete import list is:

```
__future__, json, re, sys, pathlib, typing, argparse
+ the project's own config, models, store
```

There is no `smtplib`, no `urllib`, no `http.client`, no HTTP client, no browser
automation. Nothing to send *with*.

**A runtime guard re-verifies it on every run.** `assert_no_send_path()` reads
this module's own source, strips the guard's own pattern table, and fails the
run if any send-capable construct is found:

```python
_SEND_PATH_PATTERNS = (
    "smtplib", "sendmail", "send_message(", "requests.post", "urlopen",
    "http.client", "httpx", "websocket", "selenium", "playwright",
    "pyautogui", "webbrowser",
)
```

```console
$ python -c "from jobagents.agents.outreach import assert_no_send_path; print(assert_no_send_path())"
[]
```

A grep for `smtplib|sendmail|requests.post|urlopen` returns exactly one line —
line 415, the guard's own pattern table. That single hit *is* the proof: the
only occurrence of those names in the file is the check that asserts they are
absent.

**The only writer is `Store.save_draft`.** Drafts land with `status='draft'` and
stay there. Approval and sending are outside this module's scope by design
(README §Scope boundaries: *"No auto-sending. Draft-only; a human approves every
message."*).

---

## 3. Content rules, enforced in code

Prompts are requests. These are enforced.

| Rule | Enforcement |
|---|---|
| Never invent an employer, date, metric, or skill | Prompt carries the verbatim profile; `validate_draft()` rejects a draft asserting past employment at a company absent from `profile.md` |
| **BugAgents disclosure rule** | Regex rejects `owncloud`, `gitlab`, `kubernetes`, `git-sync`, `user_ldap`, `zipslip`, `symlink`, `ldap`, `hackerone` |
| No seniority inflation | Regex rejects `staff`, `principal`, `founding`, `head of`, `director`, `vp`, `chief` constructions |
| No "disclosed / accepted / paid / resolved" BugAgents claims | Regex rejects those claim phrasings |
| No production-users / revenue / adoption claims | Regex rejects possessive, quantity, and generated-value constructions |

`validate_draft(text, kind=None, allowed_companies=None) -> (ok, violations)`
returns a list of short violation strings. An invalid draft is **not persisted**
and the reason goes into the run's `errors` — a silent rejection would be
indistinguishable from a model that produced nothing.

Two subtleties worth recording, both found by testing:

- **The target company is not a fabricated employer.** Naming the company you
  are applying *to* is the point of personalisation. `allowed_companies` exempts
  it. Without this every honest draft fails.
- **Word boundaries matter.** `ldap` must not match inside `user_ldap` twice, but
  must still catch `LDAP` and `(ldap)`. The pattern uses
  `(?<![a-z0-9])term(?![a-z0-9])`.

---

## 4. What Phase 5 checks

| Check | Kind | Detail |
|---|---|---|
| `content` | hard | Delegates to `validate_draft` — the reviewer tests the *same* invariant the generator was held to, so the two cannot drift |
| `length` | hard | Email 80–250 words; DM ≤300 chars; email must contain a contact detail |
| `employers` | hard | Past-employment phrasing naming a company not in `profile.md` |
| `withheld_terms` | hard | Re-run independently so `checks_json` names *which* term leaked |
| `seniority` | hard | Independent re-run |
| `overclaims` | hard | Adoption / revenue / disclosure claims |
| `duplicates` | hard | Cross-job near-duplicate via Jaccard token overlap, ≥0.60 |
| `rate_limit` | hard | >2 distinct **roles** per company per run |
| `personalization` | soft | Does the draft name its company, role, and matched keywords? |

Verdicts: `pass` (all hard checks clean, nothing ambiguous) · `warn` (no hard
violation but a soft signal needs a human eye) · `fail` (≥1 hard violation).

Every verdict is persisted to `reviews` with `subject_type='draft'`,
`subject_id`, `verdict`, and a `checks_json` carrying the full per-check detail.

### Near-duplicate detection

```python
jaccard(a, b) = |tokens(a) ∩ tokens(b)| / |tokens(a) ∪ tokens(b)|
```

on normalized tokens of ≥4 characters, threshold **0.60**. Drafts for the same
`job_id` are not compared (an email and its DM *should* overlap); drafts of
different kinds are not compared. Measured: identical text → 1.000, unrelated
text → 0.041.

---

## 5. Two design bugs the tests caught

Both were found by deliberately violating every invariant and checking the
verdict flipped — a checker that only ever returns `pass` is worthless, so it
has to be falsified, not spot-checked.

**1. The rate limit was unsatisfiable.** It counted draft *rows* per company,
capped at 2. But one application writes two rows (email + DM), so any company
that received even a single application was permanently in violation. Fixed to
count distinct **roles** — which is what "don't spam one recruiter" actually
means.

**2. The overclaim check flagged honest drafts.** It matched the bare noun
`revenue` anywhere, so every application to *"Analytics Engineer II, Full Stack
(Revenue Analytics)"* failed, as did the legitimate domain phrase "revenue data
modeling". A check that fails honest drafts trains the operator to ignore the
verdict, which is worse than having no check. Fixed to require a *claim
construction* — a possessive, a quantity, or a generated-value verb.

**3. Outreach drafted the same role repeatedly.** Affirm advertised one opening
in both Spain and Poland as two `jobs` rows. Outreach drafted both, producing
four near-identical applications to one company. Fixed by collapsing on
`store.make_dedupe_key` — the two-layer dedupe already knows these are one
opportunity, since `dedupe_key` is `company|title` with location deliberately
excluded — and by capping at `max_per_company` roles so outreach cannot
manufacture drafts that review is guaranteed to reject.

---

## 6. Verified results

Real run against `data/jobagents.db` (7,546 jobs, 21,861 match records).

**Outreach — 6 jobs, 12 drafts:**

```
threshold >= 65.0  track=all  limit=6 jobs
candidate matches above threshold: 120

  [ 92.86] Senior Data Analyst @ mongodb
           email        saved  (847 chars)
           linkedin_dm  saved  (176 chars)
  [ 89.87] Member of Data Staff (Analytics Engineer) @ perplexity
           email        saved  (836 chars)
           linkedin_dm  saved  (233 chars)
  [ 89.50] Agentic AI Engineer @ elastic
           email        saved  (762 chars)
           linkedin_dm  saved  (222 chars)
  [ 89.16] Analytics Engineer II, Full Stack (Revenue A @ affirm
           email        saved  (815 chars)
           linkedin_dm  saved  (188 chars)
  [ 89.16] Analytics Engineer II, Full Stack (Revenue A @ affirm
           SKIP  same role already drafted
  [ 87.02] Staff Security Engineer, Enterprise AI @ affirm
           email        saved  (874 chars)
           linkedin_dm  saved  (240 chars)
  [ 87.02] Staff Security Engineer, Enterprise AI @ affirm
           SKIP  same role already drafted

  jobs drafted     6
  drafts written   12  (email=6, linkedin_dm=6)
  rejected by code 0
  skipped          2 duplicate role(s), 0 over company cap
```

**Review — 12 drafts, 12 pass:**

```
  checked   12
  pass      12
  warn      0
  fail      0
  escalated 0
```

`escalated 0` is correct here: every draft was clean *and* unambiguous, so no
judgment call existed to escalate. The escalation path was verified separately
against a deliberately generic draft, where it returned
`tone_ok=False, fit_ok=True` with the note *"the pitch is too generic and lacks
specific achievements or company context."*

---

## 7. Limitations

Stated plainly, because the honest scope of a check matters more than its
verdict.

- **The reviewer cannot detect a well-written fabrication.** It catches
  structural violations — a named employer, a withheld term, a duplicate. A
  confidently-stated false metric that is *shaped* like a real one passes. The
  prompt carries the verbatim profile and the profile is the ground truth, but
  no code here diffs generated prose against the metrics table claim by claim.
  That is Phase 3's `tailor` guard's job, and even there it is partial.
- **`check_personalization` is not reliable enough to be a hard check.** Keyword
  matching is substring-based on the normalized body, so a draft that
  paraphrases "data modeling" as "data models" is falsely flagged. It defaults
  to a *soft* signal (WARN). `--strict-personalization` promotes it to hard, and
  should only be used once that false-positive rate is acceptable.
- **`agy` needs a permission that headless mode cannot grant.** When the model
  responds with a tool call, the run fails with a permission error. The code
  treats this as `model-unavailable` and stays with the code verdict rather than
  silently passing — but it means escalation is best-effort, not guaranteed.
- **Escalation costs a model call and ~20–25s.** With the ambiguity gate, a
  healthy run makes zero calls.
- **Duplicate detection is lexical.** Two drafts that say the same thing in
  different words score low on Jaccard and both pass. It catches template reuse,
  which is the common failure, not paraphrase.
- **The rate limit is per run, not per company over time.** Running outreach
  twice with a cleared `drafts` table can produce more than 2 drafts for one
  company overall. The cap is a per-run spam guard, not a global quota.
- **Nothing here sends, approves, or tracks replies.** Drafts are rows in
  `drafts` with `status='draft'`; the send path does not exist in this phase.
- **Draft quality is bounded by `call_omp`/DEEPSEEK.** The prompt constrains
  facts and the validator rejects violations, but voice and specificity vary
  between runs.
