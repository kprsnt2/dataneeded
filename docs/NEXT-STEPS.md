# JobAgents — What To Do After The Pipeline Is Built

**Question this answers:** "The pipeline is finished. Now what?"

**Date:** 2026-10-06 · **Workspace:** `D:\JobAgents`

The build is done. Phases 0–7 are verified (PLAN.md §12–15), the daily task is
registered at 09:00 IST, and the three project sites are live:
`job.kprsnt.in`, `agent.kprsnt.in`, `bug.kprsnt.in`.

**The pipeline does not find you a job.** It manufactures a short, high-quality
list of targets and the artifacts to approach them with. Everything downstream of
"draft written" is still yours. This document is that downstream.

---

## 0. Where the machine actually stops

Before the loops, be precise about the boundary, because the whole plan follows
from it.

| Stage | Automated? | Evidence |
|---|---|---|
| Source jobs | ✅ unattended, 09:00 IST | `scripts/run_daily.ps1`, docs/AUTOMATION.md |
| Score / match | ✅ deterministic, zero model calls | `jobagents/matching.py` |
| Tailor resume | ✅ + code-enforced anti-fabrication guard | `jobagents/tailor.py` |
| Draft outreach | ✅ draft-only, no send path in code | `jobagents/agents/outreach.py` |
| Review drafts | ✅ 11 code invariants | `jobagents/agents/review.py` |
| **Approve** | ❌ **you** | `POST /api/drafts/<id>` `{"action":"approve"}` |
| **Send** | ❌ **you, by hand** | `drafts.sent_at` is never written anywhere |
| **Track the outcome** | ❌ **nothing exists** | see §3.1 |

Latest verified run (`logs/last-run.json`, 2026-10-05):

```
jobs_total                7549        resumes_written      1
jobs_last_24h              188        drafts_pending       7
jobs_last_7d              2124        drafts_approved      0
matches_above_threshold    274        reviews_failed       0
```

Read that honestly. **274 matches above threshold, 7 drafts pending, 0 approved.**
The queue is already full and untouched. Your bottleneck today is not sourcing —
it is that nothing has been sent. Step 1 of the daily loop fixes that.

---

## 1. The daily 10-minute loop

Do this every morning. Ten minutes, in this order.

### Step 1 — Did the run happen? (30 s)

The 09:00 task may have been skipped if the laptop was off (it catches up, but
late). Check the machine-readable result first:

```powershell
Get-Content logs\last-run.json | ConvertFrom-Json | Format-List
Import-Csv logs\daily-history.csv | Select-Object -Last 5 | Format-Table
```

Look at `exit_code` (want `0`), `duration_s` (a real run is minutes, not
seconds), and `summary.drafts_pending`.

Confirm the task itself is healthy:

```powershell
schtasks /Query /TN "JobAgents-Daily" /V /FO LIST
```

Check `Status` is not `Disabled`, and read `Last Run Time` / `Last Result`. If the
run did not happen, either run it now through the same wrapper the task uses, or
force the task:

```powershell
powershell -ExecutionPolicy Bypass -File scripts\run_daily.ps1
schtasks /Run /TN "JobAgents-Daily"
```

Full troubleshooting: docs/AUTOMATION.md and docs/USER_GUIDE.md §24.

### Step 2 — Open the dashboard (30 s)

```powershell
python -m jobagents web --port 8787
```

Then open `http://127.0.0.1:8787`. Five tabs: Analytics, Jobs, Resume Studio,
Review Queue, Runs. Leave it running; `Ctrl-C` stops it.

### Step 3 — Work the Review Queue (5 min)

Go to the **Review Queue** tab. It lists every draft with `status='draft'`. Each
card shows the job, the recipient, the subject, the body, and the posting link.

For each draft: read it, then press **Approve draft** or **Reject**.

Read them properly. The reviewer already passed them through 11 code invariants
(`reviews_failed: 0`), but the invariants check *structure* — no fabricated
employer, no inflated seniority, rate limit respected, keyword coverage in range.
They cannot check whether the message is *good*. That judgment is the one thing
you are here for.

### Step 4 — Send it yourself (3 min)

**This is the step the tool refuses to do, on purpose.**

Approve flips `status='approved'` and stamps `approved_at`. It does not send.
`sent_at` exists as a column and **is never written by any code in this repo** —
verified by grepping the whole tree: it appears only in the schema
(`jobagents/store.py:78`) and as a read-only field in the dashboard payload
(`jobagents/web.py:368,444`). `POST /api/drafts/<id>` accepts exactly two
actions, `approve` and `reject`; `{"action":"send"}` returns HTTP 400.

So: copy the approved body out of the dashboard and send it from your own email
or LinkedIn. Every message. By hand.

Why this is non-negotiable: LinkedIn and X automate-detection bans are real and
account-ending (PLAN.md §9, §10). The draft-only invariant is the entire reason
running this pipeline is safe. Do not "fix" it.

### Step 5 — Record what you applied to (1 min)

**Be aware: there is no supported place to write this.** The `applications` table
exists in the schema (`jobagents/store.py:93-100`) but **no stage ever inserts
into it** — a full-tree grep for `applications` / `applied_at` finds only the
schema and PLAN.md's own diagram. PLAN.md §6 says the Jobs tab can "mark
applied/rejected"; the implemented API has no such route (`jobagents/web.py` only
exposes `GET /api/jobs` and `GET /api/jobs/<id>` — there is no write endpoint for
jobs). That is a doc-vs-code gap, not a feature.

Until it is fixed (§3.1), record applications **outside the tool** — a
spreadsheet or `notes\applications.md` — with at minimum:

| Column | Example |
|---|---|
| Date sent | 2026-10-06 |
| Company / role | Elastic — Agentic AI Engineer |
| Job id | 3080 (from the dashboard's provenance block) |
| Channel | email / LinkedIn DM |
| Follow-up due | 2026-10-12 (sent + 6 days) |

The job id matters: it is the join key back to `jobs.id`, so this sheet can be
imported the moment the tracking gap is closed. Write the id down now and the
future migration is a five-minute script instead of an archaeology project.

### Step 6 — Read the generated resumes (1 min)

```powershell
Get-ChildItem generated\ | Sort-Object LastWriteTime -Descending | Select-Object -First 5
```

Files are named `<company>__<title>__<job_id>.md` (`jobagents/tailor.py:397`).

Open the ones for the jobs you just applied to. Check that the facts, numbers,
and titles are true.

**If a fact is wrong: do not edit the generated file.** It is regenerated on the
next run and your edit is lost. Fix the source of truth — `config/profile.md` —
and re-run. If the fact is true but missing, add it to the **Verified Metrics**
table in `profile.md`. If the fact is false, change nothing: the guard should have
caught it, and `stats["rejections"]` is how you find out it did not
(docs/USER_GUIDE.md §21).

Edit `profile.md` from the **Resume Studio** tab, which backs up the previous
version to `config/.backups/` before every write. Or use the CLI and take your own
copy first:

```powershell
Copy-Item config\profile.md config\profile.backup.md
```

**Daily loop, condensed:**

```
check last-run.json  →  web --port 8787  →  Review Queue  →  approve
                     →  SEND BY HAND     →  log it in your sheet
                     →  read generated\  →  fix profile.md, never the output
```

---

## 2. The weekly loop

Once a week — pick a fixed slot, e.g. Monday after the daily loop.

### 2.1 Two runs with the slow flags

`--linkedin` and `--search` add the sources the ATS boards miss. They are slow and
`--search` spends model calls, so use them **twice a week, not daily**
(docs/USER_GUIDE.md §13, §25).

```powershell
python -m jobagents run --since 7d --linkedin --search
```

LinkedIn earned its place in the build: it surfaced India roles (Accenture, Optum,
Qualys, Albertsons, UST) that the ATS boards missed entirely (PLAN.md §12).
`--search` is what reads X and Indeed through the search index with no login and
no ban risk (PLAN.md §15).

### 2.2 Tune the threshold — this is the dial

Open the **Analytics** tab and read the **score distribution histogram**. It
buckets every match row into 10-point bands and draws a dashed marker at the
configured `auto_tailor` threshold.

Current setting (`config/keywords.md:87-90`):

```yaml
thresholds:
  auto_tailor:       65     # score >= this gets a tailored resume
  notify_only:       40     # 40-64 appears in the dashboard, no tailoring
  discard:           40     # below this is archived
```

How to read it:

| Symptom in the histogram | What it means | Action |
|---|---|---|
| Huge mass just above 65, `resumes_written` stuck at 1 | Threshold admits far more than `--tailor-limit` can process | Raise `auto_tailor` (70–75) **or** raise `--tailor-limit` |
| Very few bars right of the marker | Threshold is too high; real fits are being discarded | Lower `auto_tailor` toward 60 |
| Everything bunched at 40–55 | The keyword lists are too generic, not the threshold | Fix the must-have keywords, not the number |

That is the honest reading of the current run: **274 matches above threshold but
only 1 resume written.** The default `--tailor-limit 10` and a 274-deep queue are
not in balance. Either raise the limit deliberately or raise the bar — but do not
leave it as it is and assume the machine is working the list. It is not; it
processes 10 per run and the queue grows.

Edit thresholds in the **Resume Studio** tab — it writes a backup to
`config/.backups/` first and its **Save & verify parse** button re-parses the file
from disk with the real `load_keywords()`, which is the check you want. Or edit
directly and take your own copy first:

```powershell
Copy-Item config\keywords.md config\keywords.backup.md
# edit config/keywords.md, then rescore so the change takes effect:
python -m jobagents match --top 20
```

The dashboard reads the threshold live from `config/keywords.md`, so the histogram
marker and the funnel move on the next page load.

### 2.3 Read the rejections

A rejected resume is the anti-fabrication guard firing — the resume was **not
written** because it failed validation against `config/profile.md`
(`jobagents/tailor.py`, `run_tailor` → `stats["rejected"]`).

```powershell
python -m jobagents summary --pretty
```

Ask one question per rejection: **was the model wrong, or is the profile
incomplete?**

- **Profile incomplete** → a true fact exists but is not in `profile.md`, so the
  guard had no ground truth to validate against. Add it to the Verified Metrics
  table.
- **Model misbehaved** → it invented an employer, a figure, or a seniority level.
  This is exactly what the guard is for; do nothing except note the rate. The
  build caught two real model outputs doing this, including one that attributed
  BugAgents / AI Eco / Awakening / BrandXY to Black Piano as employment
  (PLAN.md §13). Prompt rules are not guards.

### 2.4 Read the funnel

Analytics → **Funnel**: `Sourced → Matched → Auto-tailor → Drafted → Approved`
(defined in docs/DASHBOARD.md §1). It shows the conversion percentage between
each stage. Wherever the percentage collapses, that is the week's work:

| Collapse | Diagnosis |
|---|---|
| Sourced → Matched | Keywords/thresholds are wrong, or the sources drifted |
| Matched → Auto-tailor | Threshold too high for the market |
| Auto-tailor → Drafted | `--draft-limit` too low, or the model is failing drafts |
| **Drafted → Approved** | **You are not working the queue.** This is the usual one. |

The funnel ends at **Approved**. There is no "Sent" and no "Replied" stage,
because the system has no idea either of those happened. Which is §3.1.

**Weekly loop, condensed:**

```
run --since 7d --linkedin --search   →  read the histogram, tune auto_tailor
→  read rejections, fix profile.md   →  read the funnel, find the collapse
```

---

## 3. Highest-leverage next work, ranked

Ranked by (value unlocked) ÷ (effort). The first one is not close.

### 3.1 — Close the loop on outcomes **(do this first)**

**The gap, stated plainly:** the pipeline optimizes sourcing → outreach and
measures *nothing* after send. There is no reply tracking, no status field that
anything writes, no way to answer "did any of this work?"

The evidence, checked in the code rather than assumed:

| Claim | Verification |
|---|---|
| `applications` table exists | `jobagents/store.py:93-100` — `id, job_id, status, applied_at, notes` |
| Nothing writes to it | Full-tree grep for `applications`/`applied_at` → only the schema and PLAN.md's diagram |
| No send tracking | `drafts.sent_at` (`store.py:78`) is read-only; never written (`web.py:368,444`) |
| No reply tracking | No table, column, or code path for replies anywhere |
| Dashboard cannot record it | No `POST` route for jobs; only `/api/drafts/<id>` and `/api/config/<name>` accept writes |

**Why this is #1:** every other improvement compounds on a number you cannot
currently see. You cannot tell whether 65 is the right threshold, whether the
email or the LinkedIn DM converts, or whether tailoring helps at all. Right now
the pipeline can run perfectly forever and you would learn nothing. Every
application you send without recording it is an experiment you threw away.

**What to build (small — the schema is already there):**

1. A `POST /api/applications` route in `jobagents/web.py` that upserts
   `(job_id, status, applied_at, notes)` — the table and its `UNIQUE(job_id)`
   constraint already exist, so this is one handler and one `Store` method.
2. An "Applied" button on the Review Queue card, right after Approve, so the
   action you already take in Step 4–5 has somewhere to land.
3. Two stages added to the funnel: **Sent** (`COUNT(*) FROM applications`) and
   **Replied** (`status IN ('replied','interview','offer')`).
4. A `status` vocabulary fixed up front — `applied`, `replied`, `interview`,
   `take_home`, `offer`, `rejected`, `ghosted`. Without a fixed vocabulary the
   data is unqueryable within a month.

Until it exists: keep the §1 Step 5 sheet. The job id is the join key.

### 3.2 — A follow-up cadence

**The gap:** nothing reminds you to follow up. `applications.notes` is a free-text
field, not a scheduler; there is no date arithmetic anywhere in the pipeline; the
09:00 task only runs sourcing.

A single polite follow-up at **day 5–7** is the highest-yield human action in a
job search and it is the one most often skipped, because it depends on memory.
The current design guarantees it gets skipped: `sent_at` is never written, so
there is not even a timestamp to count from.

**Depends on 3.1** — you cannot schedule a follow-up from a date the system does
not record. Once `applications.applied_at` is populated, the follow-up is a
trivial query:

```sql
SELECT j.title, j.company, a.applied_at
FROM applications a JOIN jobs j ON j.id = a.job_id
WHERE a.status = 'applied'
  AND a.applied_at <= datetime('now', '-5 days');
```

Surface that as a banner in the dashboard, or as a line in the daily summary.
One follow-up, then stop — two is the limit before it reads as pressure.

### 3.3 — Interview and take-home support

**The gap:** the pipeline stops at outreach. There is no interview prep, no
take-home scaffolding, no company brief.

This is a genuinely different capability from anything built so far, and it is
where the next real leverage sits — a tailored resume gets you the conversation,
and then the conversation is unassisted. The highest-value version is narrow:
for a given `job_id`, generate a one-page brief from the stored JD
(`jobs.description`, already in the database) plus the match reasons
(`matches.reasons_json`, `matched_keywords`, `missing_keywords`) — what they
will probe, which of your verified metrics to lead with, and which required
keyword you cannot honestly claim.

Note that `missing_keywords` is already computed and stored for every match. It
is currently only shown in the dashboard's expandable reasons row. It is a
ready-made interview-prep input that nothing consumes.

### 3.4 — Keep the three live sites and the resume claims in sync

The resumes now cite `job.kprsnt.in`, `agent.kprsnt.in`, and `bug.kprsnt.in`.
Those URLs are now **load-bearing claims on a job application.** A recruiter who
clicks a dead link learns something worse than nothing.

| Asset | What it must keep showing | Failure mode |
|---|---|---|
| `job.kprsnt.in` | JobAgents, with current verified numbers | Stale counts contradict the resume |
| `agent.kprsnt.in` | AgentSwarm | Down = broken link on a live application |
| `bug.kprsnt.in` | BugAgents, **disclosure-safe** | See §3.5 — this one has a legal edge |

Two concrete rules:

1. **Any number that appears on a resume must be regenerable from this repo.**
   The static snapshot exists for exactly this — `python -m jobagents export
   --out site/index.html` (`jobagents/export.py`) writes a self-contained HTML
   file with aggregate numbers, no personal data, no individual job rows. When
   `logs/last-run.json` changes materially, re-export and redeploy. The resume
   and the site then cannot disagree.
2. **Re-verify the links, not just the servers.** An HTTP 200 on the domain root
   is not proof the deep link in the resume resolves. Check the exact URLs the
   resumes cite.

This is a recurring task, not a one-off: it goes in the weekly loop.

### 3.5 — BugAgents disclosure follow-through **(real deadline risk)**

**The gap:** three submission-ready reports exist and **none has been
submitted.** Submission is a manual, out-of-band action that no part of this
system performs or reminds you about.

This is the most time-sensitive item in this document, and it is not a
"nice to have" — it has a hard expiry that nothing in the repo tracks:

- **Programs close.** A bounty program that is open today can stop accepting
  reports, reduce scope, or shut down entirely.
- **Duplicates land first.** A valid finding reported second is worth zero. The
  value of a vulnerability report decays toward zero the longer it sits
  unsubmitted, and it decays fast.
- **Disclosure obligations run on their own clock.** The longer a finding sits
  unreported, the worse the position if the issue is independently discovered.

Two rules that are already stated in the repo and must not be relaxed while you
do this:

- **Do not disclose BugAgents findings publicly.** docs/USER_GUIDE.md §28 rule 5:
  the reports are not public. `bug.kprsnt.in` must show the *work*, not the
  *findings* — no target names, no vulnerability detail, no reproduction steps
  before coordinated disclosure. The tailor guard already enforces a
  disclosure-safety check on resume text (`jobagents/tailor.py`); the site has no
  such guard, so it is on you.
- **Submit, do not publish.** Submission is to the program's own channel.

Put this on a calendar with the program's actual close date, not on the daily
loop — it is a deadline, not a routine.

---

## 4. What NOT to do

These are the design boundaries. Each one is load-bearing; removing it does not
make the tool better, it makes it dangerous.

| Don't | Why | Where it is enforced |
|---|---|---|
| **Add an auto-send path** | LinkedIn/X automation bans are real and account-ending. The draft-only invariant is the reason running this is safe. | `assert_no_send_path` audits the module's own source at runtime; `{"action":"send"}` → HTTP 400 |
| **Bind the dashboard beyond 127.0.0.1** | Single-process, **no auth**. Anyone who reaches the port has full control, including config writes. | `--host` defaults to `127.0.0.1`; docs/DASHBOARD.md §Security |
| **Commit resume data or API keys** | This repo must never contain personal resume data. The key is injected at runtime from `~/.pi/agent/auth.json` so no secret sits in the task definition. | `.gitignore` (`resume/`, `generated/`, `data/`, `*.pdf`, `*.docx`); `scripts/run_daily.ps1` |
| **Edit a generated resume to fix a fact** | It is regenerated on the next run; the edit is lost and the wrong fact returns. | Fix `config/profile.md` instead (docs/USER_GUIDE.md §21) |
| **Publish BugAgents findings to make the site look better** | Reports are not public until coordinated disclosure. | docs/USER_GUIDE.md §28 rule 5 — **human-enforced** |
| **Put the Fireworks key in a file in this folder** | Same as the git rule; the wrapper injects it from outside the repo. | docs/USER_GUIDE.md §28 rule 3 |

Verify the privacy boundary before any push:

```powershell
git status --short            # must show no resume/ or generated/ paths
git check-ignore -v resume/   # must report .gitignore:N:resume/
```

---

## 5. Next 7 days — the checklist

Day 1 is the only one that matters if you do nothing else.

### Day 1 — Clear the queue

```powershell
cd D:\JobAgents
python -m jobagents doctor
Get-Content logs\last-run.json | ConvertFrom-Json | Format-List
python -m jobagents web --port 8787
```

In the browser at `http://127.0.0.1:8787`:

- [ ] **Review Queue** → approve the 7 pending drafts
- [ ] **Send all 7 by hand.** Email or LinkedIn, yourself.
- [ ] Start your applications sheet: date, company, role, **job id**, channel,
      follow-up date (+6 days)

```powershell
Get-ChildItem generated\ | Sort-Object LastWriteTime -Descending | Select-Object -First 5
```

- [ ] Read the generated resumes; fix any wrong fact in `config/profile.md`, never
      in the generated file

### Day 2 — Fix the threshold/limit mismatch

- [ ] **Analytics** tab → read the histogram against the `auto_tailor` marker
- [ ] Decide: raise `auto_tailor`, or raise `--tailor-limit`. 274 queued against a
      limit of 10 is not a working configuration.
- [ ] Edit `config/keywords.md` (Resume Studio backs it up automatically), or:

```powershell
Copy-Item config\keywords.md config\keywords.backup.md
python -m jobagents match --top 20    # rescore with the new threshold
```

- [ ] Run the pipeline with a deliberate limit:

```powershell
python -m jobagents run --since 24h --tailor-limit 20 --draft-limit 20
```

### Day 3 — Weekly deep run

```powershell
python -m jobagents run --since 7d --linkedin --search
python -m jobagents summary --pretty
```

- [ ] Check `reviews_failed` and `resumes_written` in the new summary
- [ ] Work the new queue the next morning (daily loop)

### Day 4 — Start the outcome-tracking work (§3.1)

- [ ] Add a `Store` method to upsert into `applications` — the table and its
      `UNIQUE(job_id)` already exist, so no migration is needed
- [ ] Add `POST /api/applications` to `jobagents/web.py`
- [ ] Add an **Applied** button to the Review Queue card
- [ ] Add **Sent** and **Replied** to the funnel
- [ ] Fix the PLAN.md §6 claim that the Jobs tab marks applied/rejected — either
      build it or correct the doc

### Day 5 — Portfolio consistency (§3.4)

```powershell
python -m jobagents export --out site/index.html
```

- [ ] Re-export the static snapshot with current numbers and redeploy
      `job.kprsnt.in`
- [ ] Click the exact URLs cited on your resumes: `job.kprsnt.in`,
      `agent.kprsnt.in`, `bug.kprsnt.in`
- [ ] Confirm `bug.kprsnt.in` shows work, not findings — no target names, no
      vulnerability detail

### Day 6 — BugAgents submissions (§3.5)

- [ ] Look up the **actual close date** for each of the 3 programs
- [ ] Submit report 1. Then 2. Then 3. Same day.
- [ ] Put each program's close date on a calendar, not in this repo

### Day 7 — Follow-ups and review

- [ ] Follow up on anything sent ≥ 5 days ago and still silent (from your sheet)
- [ ] Read the funnel. Where did it collapse? That is next week's work.
- [ ] Confirm the 09:00 task is still healthy:

```powershell
schtasks /Query /TN "JobAgents-Daily" /V /FO LIST
```

---

## 6. The one-paragraph version

The machine sources, scores, tailors, and drafts — unattended, every morning at
09:00. It will never send anything, and it will never tell you what happened
after you did. So: **every morning, open the dashboard, approve the drafts, send
them by hand, and write down what you sent.** Once a week, run the slow sources,
move the threshold against the histogram, and read the funnel. Then fix the thing
that is actually broken — which is that the pipeline measures the top of the
funnel precisely and the bottom of it not at all. And submit the three BugAgents
reports before someone else does.

---

*Related: [README.md](../README.md) · [PLAN.md](../PLAN.md) ·
[docs/USER_GUIDE.md](USER_GUIDE.md) · [docs/AUTOMATION.md](AUTOMATION.md) ·
[docs/DASHBOARD.md](DASHBOARD.md)*
