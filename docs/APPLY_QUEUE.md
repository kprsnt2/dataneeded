# Apply Queue, Eligibility Gate & Cold Outreach

Three stages added on top of the existing pipeline. **None of them submits or
sends anything.** The pipeline's draft-only guarantee is unchanged; what changed
is how much work is left for you.

```
sourced → matched → tailored → drafted → reviewed
                                      ↓
                            [PHASE B] eligible?     ← deterministic gate
                                      ↓ ready
                            [PHASE A] packaged      ← resume + letter + answers
                                      ↓
                              you submit (~2 min)

separately:  [COLD OUTREACH] recruiter emails + startup founder emails
```

---

## Phase B — `jobagents apply-gate`

Decides which jobs may enter the application queue. No model calls: every check
is a pure function of stored state (plus one optional HTTP HEAD), so a verdict is
reproducible and testable.

```bash
python -m jobagents apply-gate --limit 25 --since 30d
python -m jobagents apply-gate --no-network            # skip liveness probe
```

| Check | Passes when | Notes |
|---|---|---|
| `score` | match score ≥ `auto_tailor` (65) | |
| `location` | posting is in **India** | the single biggest filter |
| `role_dedupe` | role not already queued | company+title, seniority stripped |
| `company_cap` | < 1 real application to that company in 7 days | **only submitted applications count** |
| `freshness` | posted ≤ 21 days ago | unknown age is `?`, not a fail |
| `liveness` | apply URL returns 200 | 403/405 is `?` not a fail |
| `route` | ATS recognised | `gh_jid=`, ashby, lever, workday… |
| `resume` | tailored resume exists **on disk** | not just a DB row |
| `education` | no strict CS/Engineering degree demand | never auto-fails |
| `compensation` | no salary floor configured, or floor met | |

**Three states, not two.** `ok` / `fail` / `unknown`. `unknown` never rounds up to
"ready" — an application with any open question is still packaged, but it is
listed as a handoff item rather than assumed fine.

### Why location is an allowlist, not a blocklist

The first version enumerated ~25 foreign countries and treated anything
unrecognised as `unknown` (passable). It classified **Costa Rica**, **EMEA** and
**Remote, US** as fine. Now:

- India named → `india`
- any recognised non-India country/region, **or** a two-letter region code
  (`Remote, US`, `Austin, TX`, `Toronto, ON`) → `foreign` → **fail**
- a multi-location posting naming India *and* elsewhere
  (`Bangalore, India; Remote, Poland`) → `foreign` → **fail**
- bare `Remote` / `Anywhere` → `unknown` → needs confirmation (pass with
  `--allow-global-remote` if you want to opt in)
- nothing stated → `unknown`

A missing country in this design causes a *false block* (safe); a missing country
in a blocklist causes a *false pass* (unacceptable).

---

## Phase A — `jobagents apply-queue`

Builds one Markdown package per gate-approved job in
`generated/applications/<company>__<title>__<id>.md` containing:

- the tailored resume already on disk, plus its `.html` / `.pdf` / `.docx` siblings
- the existing outreach email draft
- a **cover letter**, run through the same anti-fabrication validator as outreach
- a **question sheet** — every ATS question that can be answered from verified
  ground truth, with the rest explicitly marked OPEN
- the direct apply URL and route (Greenhouse/Ashby/Lever = fast lane; Workday/
  iCIMS/Taleo/LinkedIn = manual)

```bash
python -m jobagents apply-queue --limit 10
python -m jobagents apply-queue --limit 5 --no-letter   # no model calls
```

### The question sheet is the anti-fabrication surface

`config/application_answers.md` (gitignored; copy the `.example.md` template)
holds the facts a form asks for that a resume cannot supply — notice period,
expected CTC, work authorisation. Anything left as `<...>` stays **OPEN** and
appears in the handoff checklist.

Why this matters: a form-filler that runs out of facts invents them. The queue
never does — it prints a checklist of what a human must supply.

---

## Cold outreach — `jobagents cold-outreach`

The application-attached email already existed. This adds the two other channels.

```bash
python -m jobagents cold-outreach --kind recruiter --limit 5   # roles naming a TA contact
python -m jobagents cold-outreach --kind founder   --limit 5   # YC companies
python -m jobagents cold-outreach --kind both
```

### Recruiter emails

Eligible only for postings that **name a recruiter/talent contact**. Recipient
extraction is deliberately honest:

| Posted text | Name | Address |
|---|---|---|
| "contact Jane Smith, Technical Recruiter at jane.smith@acme.com" | Jane Smith | jane.smith@acme.com |
| "Reach out to our Recruiter: David Chen for details." | David Chen | *(none)* |
| "Contact our support team at support@acme.com" | *(none)* | *(none)* |

There is **no address guessing.** A wrong `firstname.lastname@` guess is a spam
complaint; "(no address — find the person)" is the honest output.

### Founder emails

Targets companies from `config/yc_companies.txt` (10,711 companies) already in
the pipeline, grounded in their top-scoring posting. Recipient is always left for
you — use the company's YC contact form or the founder's public address.

### Code-enforced content rules

Applies to both channels, on top of `outreach.validate_draft`:

- `invented referral`, `invented prior meeting`, `claims to be a product user`
- `asserts they are hiring` when the posting does not say so
- company must be named
- 70–260 words; must carry a real signature
- `claims-employee-status`
- **filler openings** — "I am reaching out", "I noticed/saw", "I came across",
  "I hope this email finds you". These were only in the prompt at first and the
  model used them on 3 of 3 first drafts. A rule that lives only in a prompt is
  not a rule; it is a suggestion, so it became a validator check.

A draft that fails is retried **once** with the specific violation fed back, then
rejected. Rejecting outright wasted full model calls on drafts that were fine
except for the opening sentence.

---

## Wiring into the daily run

`STAGES` is now
`source, match, tailor, outreach, review, gate, pack, export, render`:

```bash
python -m jobagents run --gate-limit 40 --apply-limit 5
```

The `gate` stage runs after `tailor` so the resume check has something to check.

---

## Verification

Both new modules are tested by **falsification** — every rule is deliberately
violated and must fire:

```bash
python scripts/test_apply_gate.py      # 63 checks
python scripts/test_cold_outreach.py   # recipient + content rules
```

Both also audit their own source for submission/sending capability at runtime
(`assert_no_apply_path`, `assert_no_send_path`), the same pattern as
`agents/outreach.py`. Verified both ways: clean on the real module, and firing on
a copy with `requests.post` injected.

---

## Bugs found and fixed while building this

Listed because the pattern matters: every one was found by reading real output,
not by the tests passing.

| # | Bug | Symptom | Fix |
|---|---|---|---|
| 1 | `candidates()` picked `MAX(m.id)` (newest track) not best score | gate pool filled with 26–39 point rows, all immediately blocked | select `MAX(m.score)` per job |
| 2 | Blocked rows excluded jobs from re-gating | a job blocked for a missing resume never returned after tailoring | only real applications exclude |
| 3 | `company_cap` counted gate rows as applications | blocked 28 of 40 candidates on first live run | count only submitted applications |
| 4 | Education regex expected `Bachelor's` after `normalize_text` stripped apostrophes | rule could never match | `bachelor\s*s?` |
| 5 | Location blocklist missed Costa Rica, Mexico, EMEA, `Remote, US` | **false passes** | allowlist + region-code detector |
| 6 | India matched first in multi-location strings | "Bangalore, India; Remote, Poland" passed | any non-India site disqualifies |
| 7 | Route classified by host only | MongoDB's Greenhouse URL (`?gh_jid=`) reported "unrecognised" and told you to expect 4–8 form pages | query-string markers checked first |
| 8 | Cover-letter row said OPEN in the sheet | told you to write a letter generated 8 lines above | pass the generated letter through |
| 9 | `find_recipient` captured the verb | greeting "Hi Contact Jane Smith" | strip leading verbs, trailing filler |
| 10 | `support@` / `careers@` not filtered | a cold email would be addressed to `careers@` | anchor the pattern on the local part |
| 11 | Filler openings only in the prompt | 3 of 3 first drafts opened "I am reaching out" | validator check + one retry |

---

## Operational note: importing from the repo root

Inside `jobagents/`, a **top-level** module cannot use a double-dot relative
import in this interpreter — `from ..config import x` raises
`attempted relative import beyond top-level package`. Single-dot and absolute
imports work. `jobagents/agents/outreach.py` (one level deeper) uses `..` fine;
the new top-level modules (`applications.py`, `apply_gate.py`,
`cold_outreach.py`) use absolute `from jobagents.x import y`, consistent with
the rest of the package. Isolated with a three-file package to confirm it is not
a project-specific quirk.
