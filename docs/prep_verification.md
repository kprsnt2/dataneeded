# Prep Verification — Adversarial Review of the Three Interview Prep Docs

**Verifier:** prep-verifier (task-2) · **Date:** 2026-10-12 · **Independence:** I did not write or edit any of the three files under test. This file is the only thing I wrote.

## Revisions verified (SHA256 — verified on disk, post-freeze)

| File | Lines | SHA256 | Last write |
|---|---|---|---|
| `docs/icici_lombard_interview_prep.md` | 468 | `07B46F40EAA17CEE8B1E59D10EB4206F212FA436E79191E9686813C1284206A0` | 2026-10-12 09:52:09 |
| `docs/micro1_data_analyst_prep.md` | 416 | `A9DD33590AC002179B8F523570923150FA9737F98C3255C0EDD2694673A1DE81` | 2026-10-12 09:55:24 |
| `docs/micro1_ai_agent_evaluator_prep.md` | 382 | `BAFE954169F7AE61ED8978532C575C338039C0A407D8EC9A9F77F98665ED3D29` | 2026-10-12 09:55:14 |

Re-hashed after the Lead's freeze confirmation: **all three unchanged**. Findings below are against these revisions. My first pass read earlier revisions (icici 405 lines, data-analyst 341, evaluator 297); where a finding applies only to a superseded revision I say so explicitly.

## Verdicts

| File | Verdict | Findings | Notes |
|---|---|---|---|
| `icici_lombard_interview_prep.md` | **PASS-WITH-FIXES** | 5 (0 high, 2 medium, 3 low) | Zero stale values, zero overclaims, zero misattribution. Glossary is sound. Fix the unsourced comp figure and two glossary precisions. |
| `micro1_data_analyst_prep.md` | **PASS-WITH-FIXES** | 6 (1 high, 2 medium-high, 3 low-medium) | The spreadsheet section contains a real factual error about the function it recommends, plus platform-availability traps. Everything else is accurate. |
| `micro1_ai_agent_evaluator_prep.md` | **PASS-WITH-FIXES** | 4 (2 high, 2 medium) | The §4.1 decision framework contradicts itself and two later sections — on the interview's highest-signal topic. Fixable in minutes. |
| Cross-file | **1 consistency finding** | 1 (medium) | The three "Never say" lists are not equivalent, and none carries profile rule 7's full set. |

**Nothing failed.** Specifically: **zero** STALE values (I checked every one of the 19 binding "do not use" numbers), **zero** OVERCLAIMs of seniority/publication/disclosure, **zero** MISATTRIBUTION of independent projects to an employer, and every count in the task's verification list matches `config/profile.md` exactly.

### Counts by category

| Category | Count | Where |
|---|---|---|
| STALE | 0 | — |
| OVERCLAIM (seniority / publication / disclosure) | 0 | — |
| MISATTRIBUTED (independent ↔ employer) | 0 | — |
| TECH-ERROR | 4 | data-analyst §5.1 ×2, §2.1, §5.2 |
| DOMAIN-ERROR (hard) | 0 | — |
| DOMAIN-IMPRECISION | 2 | icici §7.3 ×2 |
| INTERNAL-CONTRADICTION | 3 | evaluator §4.1 ×2, data-analyst §2.2 |
| FRAMEWORK-GAP | 1 | evaluator §4.1 |
| UNSOURCED | 3 | icici §2.4, data-analyst §0, evaluator §0/§5.3 |
| CONSISTENCY | 1 | cross-file "Never say" lists |
| IMPRECISE / INTERNAL-TENSION | 2 | icici §0.6, icici §2.4 vs §9 |

## Method and its limits (read this before weighting the audit tables)

- Read `config/profile.md` in full first; treated its "Stale values — do not use" list as binding. Cross-read `outreach_templates.md` §6 and `interview_guide.md` in full, plus both research companions (`icici_lombard_research.md`, `micro1_platform_research.md`) to test whether the prep docs' "verified" claims match the grading in the files they cite.
- Verified the two micro1 invitation quotes character-by-character against the screenshots at `docs/assets/` — **both verbatim quotes and both topic lists are accurate.**
- **`web_search` is unavailable in this session** (no `DEEPSEEK_API_KEY`) — the same block the intel-researcher recorded. I verified externally where a static page was fetchable (one success: Exceljet's XLOOKUP reference, which settles the highest-value technical finding). Microsoft's own support pages return only JS navigation chrome, and `irdai.gov.in` was already recorded as 504. **Consequence: the insurance glossary audit is a domain-knowledge audit, not a cited-source audit, except where I say otherwise.** I have flagged this honestly rather than dressing it up.

---

## Findings

Severity: **H** = would cost the interview or mislead materially · **M** = a competent interviewer could push back and win · **L** = tighten when convenient.

### F-01 · icici §2.4 — unsourced comp figure · UNSOURCED · **M**

> "**The likely mismatch.** Your stated position is remote-first with a **$150k+** expectation."

**What's wrong:** `$150k+` is not in `config/profile.md`, `interview_guide.md`, `outreach_templates.md`, or anywhere else in the repo. A repo-wide grep for `150k|$150|150,000|compensation|salary|expected rate` returns this line and nothing that sources it. It is the load-bearing premise of the whole of §2.4 (and of §0's fourth risk bullet), and it is presented as a fact about the candidate's own position. If the real floor is different, the doc's entire comp strategy is aimed at the wrong target — and the file's own rule (line 5) is "if a figure is not in that file, it does not get said out loud."

**Corrected wording:**
> "**The likely mismatch.** Your own stated position is remote-first and USD-denominated. *(No figure is quoted here on purpose: the number is not recorded in `config/profile.md`, so confirm it with yourself before you use it as a walk-away line. An unsourced number in a prep doc becomes a number said aloud.)* An India-based general insurer hiring a Data Analyst / Analytics Engineer will typically band well below a remote-USD baseline in INR terms, even at senior IC level."

### F-02 · icici §7.3 — ceding premium and the net loss ratio · DOMAIN-IMPRECISION · **M**

> "**Ceding / reinsurance** | Premium and risk transferred to a reinsurer. Affects net retained risk, and therefore net loss ratios."

**What's wrong:** the causal step is wrong as stated, and it is the kind of thing a chief actuary or a reserving lead would catch in one follow-up. Under a **proportional (quota-share) cession**, premium and claims are ceded in the same proportion, so the *ratio* is unchanged by construction: cede 30% of premium and 30% of the claims and the loss ratio is identical. What actually moves the net loss ratio is **non-proportional cover** (excess of loss, where ceded claims are not proportional to ceded premium), **ceding commission / profit share** (which changes the expense side), and **mix effects** across lines. The rest of the row ("affects net retained risk") is correct.

**Corrected wording:**
> "**Ceding / reinsurance** | Premium and risk transferred to a reinsurer. Affects net retained risk and net earned premium. Careful: a *proportional* cession reduces premium and claims together, so it does **not** by itself move the loss ratio — non-proportional cover, ceding commission and line mix are what move it."

### F-03 · icici §7.3 — loss ratio / ICR: gross or net? · DOMAIN-IMPRECISION · **L**

> "**Loss ratio** | Incurred claims divided by premium earned, for a line of business." / "**Incurred Claims Ratio (ICR)** | Claims incurred relative to premium earned over a period — the reported form of the loss ratio in Indian insurer disclosures."

**What's wrong:** neither row says **net or gross**, and in Indian general-insurance disclosures the reported ICR is the **net** incurred claims ratio (net incurred claims ÷ net earned premium, i.e. after reinsurance ceded). A general insurer's interviewer will very likely ask "net or gross?" — it is the standard follow-up, because the two numbers differ materially on a heavily-ceded book. Not an error, but an unnecessary exposure.

**Corrected wording (append to both rows):** "In insurer disclosures this is the **net** figure — net incurred claims over net earned premium. Gross is computable but is not what is reported."

### F-04 · icici §2.4 vs §9 — company comp figure asserted where §9 forbids it · INTERNAL-TENSION · **L**

§2.4: "A salary-aggregator page indicated roughly **₹11.2 L/yr** for a Data Engineer at 1–5 years at this company…" · §9 "Never say": "Any ICICI Lombard financial or compensation figure…"

**What's wrong:** the two statements are in tension, and the pocket card is the thing he will actually have in front of him. The research file grades this figure **WEAK** ("Ambiguous — treat as indicative only"; the same page also shows **16.5** among latest reported salaries, and "28% less than the Insurance industry average" — none of which the prep doc carries). A single ambiguous aggregator number is a thin basis for a structural conclusion.

**Corrected wording (append to §2.4):** "(Calibration only — **never repeat this figure to the recruiter or in the interview** (§9). The same page is internally inconsistent: it also shows 16.5 among latest reported salaries, so treat the direction as the signal, not the number.)"

### F-05 · icici §0.6 — CTO's public statements compressed · IMPRECISE · **L**

> "a CTO who has spoken publicly about AI and fraud detection since 2021"

**What's wrong:** `icici_lombard_research.md` dates the AI/Azure public work to **Jun 2021** and the fraud-detection statements to a **Jul 2024** CTO interview. The sentence merges them into a 2021 start for both. Harmless in an interview, but it is a fact about the company said to the company.

**Corrected wording:** "a CTO who has spoken publicly about AI since 2021, and about AI-driven fraud detection since at least 2024".

### F-06 · data-analyst §5.1 — XLOOKUP approximate match and sorting · TECH-ERROR · **H**

> "| Approximate / banded lookup | `XLOOKUP` with `match_mode`, or `VLOOKUP` with `TRUE` | For tiered rates and banding — **requires sorted data**. |"

**What's wrong:** this is the one factual error in the spreadsheet section, and it sits in the topic the interview explicitly tests ("Spreadsheet proficiency (baseline)"). **`XLOOKUP`'s approximate match (`match_mode` -1 = exact-or-next-smaller, 1 = exact-or-next-larger) does not require sorted data** — it scans. Sorting is required for (a) `VLOOKUP` with `TRUE`, and (b) `XLOOKUP` **binary search**, which is a different argument (`search_mode` 2 / -2). Verified externally: Exceljet's XLOOKUP reference lists `match_mode` -1/1 with no sorting requirement, and states separately that "to use binary search mode, data must be sorted in ascending or descending order… if data is not sorted properly, a binary search can return invalid results that look perfectly normal" (<https://exceljet.net/functions/xlookup-function>). Exceljet also confirms XLOOKUP is "available in Excel 2021+ and Excel 365" — which the row does not say either.

**Why it matters:** the doc's own previous row sells XLOOKUP as "preferred over VLOOKUP because it doesn't break when columns move" — then attaches VLOOKUP's sorting limitation to it. An interviewer who knows the function reads that as memorised-but-not-understood, which is exactly the failure mode the topic is designed to catch.

**Corrected wording:**
> "| Approximate / banded lookup | `XLOOKUP` with `match_mode` (-1 = exact or next smaller, 1 = exact or next larger), or `VLOOKUP` with `TRUE` | For tiered rates and banding. **`XLOOKUP`'s approximate match does not need sorted data; `VLOOKUP` with `TRUE` does** (first column ascending). Sorting is only needed for `XLOOKUP` binary search (`search_mode` 2 / -2). |"

### F-07 · data-analyst §5.1 — Excel-only functions presented as the recall set for a Google Sheets user · TECH-ERROR · **M-H**

> "| Text cleaning | `TRIM`, `CLEAN`, `SUBSTITUTE`, `TEXTSPLIT`/`TEXTBEFORE`/`TEXTAFTER` | …" · "| Power Query | — | For repeatable cleaning steps that you can refresh… |"

**What's wrong:** two separate problems.
1. **Availability.** `TEXTSPLIT`, `TEXTBEFORE` and `TEXTAFTER` are **Excel 365-only** — absent from Excel 2019/2021 and **absent from Google Sheets** (Sheets uses `SPLIT`, `REGEXEXTRACT`, `TEXTJOIN`). **Power Query** exists in Excel and Power BI and **not in Google Sheets** (the Sheets equivalents are a query sheet or an Apps Script job). The candidate's verified stack is **Google Sheets + Apps Script** (profile.md line 143), and §5.2 of this very doc — added in the current revision — instructs him to say "I work in Google Sheets rather than Excel". Naming Sheets-absent functions as his "instant recall" set therefore sets a trap that §5.2's honesty guidance then has to defuse under time pressure.
2. **The TRIM/CLEAN claim is incomplete in a way that matters.** Excel `TRIM` removes **ASCII space (char 32) only** — a non-breaking space (char 160, the classic web-pasted value) survives `TRIM`, and `CLEAN` only strips chars 0–31, so it survives `CLEAN` too. Since the row's whole point is "trailing spaces and non-printing characters are the most common cause of a lookup that 'should' work", the fix belongs in the row.

**Corrected wording (row + one added line):**
> "| Text cleaning | `TRIM`, `CLEAN`, `SUBSTITUTE` (Sheets: same, plus `SPLIT`/`REGEXEXTRACT`) | Trailing spaces and non-printing characters are the most common cause of a lookup that 'should' work. **`TRIM` only removes ASCII spaces — a non-breaking space (CHAR(160)) survives `TRIM` and `CLEAN`; the fix is `SUBSTITUTE(x,CHAR(160)," ")`.** `TEXTSPLIT`/`TEXTBEFORE`/`TEXTAFTER` are **Excel 365 only — not Excel 2019/2021 and not Google Sheets.** |"
> "| Power Query | — | **Excel / Power BI only — not Google Sheets.** For repeatable cleaning steps you can refresh rather than manual steps you redo; in Sheets that is a query sheet or an Apps Script job. |"

And add the platform rule to §5.2: *"Name the platform with the function. If the interviewer is in Excel and you are in Sheets, say which of these you have actually used rather than which you have read about."*

### F-08 · data-analyst §2.1 — the stated rationale for the DQ order does not survive one question · TECH-ERROR · **M**

> "**Say this out loud in the interview:** *"I run data quality in that order — completeness, accuracy, consistency, timeliness, validity, uniqueness — **because the cheap checks eliminate most of the problem before you spend effort on the expensive ones**."*"

**What's wrong:** the six dimensions themselves are right (this is the standard DAMA-DMBOK core set, and "the standard vocabulary of the field" is a fair claim). The **justification is not**: it presents the list as cost-ordered, but **accuracy — full reconciliation against an authoritative source of truth — is the most expensive check on the list, and it is second.** A senior interviewer asks "reconciliation is your most expensive step; why is it second?" and the answer collapses. The order is actually the conventional checklist order, not a cost ordering.

**Corrected wording:**
> "I run the six as a standard checklist — completeness, accuracy, consistency, timeliness, validity, uniqueness. Then I triage by cost: the cheap structural checks (completeness, validity, uniqueness) usually localise the problem before I spend on full reconciliation against the source, and reconciliation is the expensive one."

### F-09 · data-analyst §2.2 — the review/validation mapping is inverted · INTERNAL-CONTRADICTION · **M**

> "This is directly your ground truth. At Black Piano, the data-quality agent *is* the validation side; the audit discipline from nine years at Optum is the review side. Use both."

**What's wrong:** this contradicts (a) the definitions given two lines above it — validation is "proving a dataset meets defined rules, **with a pass/fail outcome**", and the agent does not gate anything: it detects a missing field and **repairs** it, with email escalation when it can't; (b) the same file's pocket card, "9 years CMS enrollment audit at Optum — **data quality as a gate, not a report**" (line 400); (c) `config/profile.md` line 56, "Applied **zero-tolerance quality gates**"; and (d) `icici_lombard_interview_prep.md` §8, "the Optum audit discipline is the **prevent** side". If he says the sentence aloud, an interviewer who is listening will hear him file his gate experience under "review" and his repair agent under "validation".

**Corrected wording:**
> "This is directly your ground truth, and the mapping is the reverse of the obvious one. **Optum is the gate**: zero-tolerance pass/fail on high-volume federal transactions, with audit-ready documentation — that is validation in the strict sense. **The Black Piano agent is detection and recovery**: it finds a rule violation (a required field is missing), repairs it, and escalates when it can't. Prevention is the audit habit; recovery is the agent. Use both, and say which is which."

### F-10 · data-analyst §0 — "All verified" over claims the research file grades ANECDOTAL · UNSOURCED · **M**

> "**Before anything else — the five platform facts that change how you prepare.** All verified in [micro1_platform_research.md](micro1_platform_research.md):" … item 3 "**Zara generates follow-ups from the *end* of your introduction**" … item 5 "You can ask Zara to rephrase… the transcript is live on screen and you **cannot scroll back**".

**What's wrong:** `micro1_platform_research.md` grades these **ANECDOTAL**, not VERIFIED: §B3 is explicitly "ANECDOTAL (multiple independent candidates, converging)", the intro-seeding claim rests on a single quoted candidate ("Zara typically extracts context from how you finish your intro…"), and the source table marks both the seeding post and the transcript/no-scroll-back post **ANECDOTAL** (lines 456–457). The research file's own closing line is: "All ANECDOTAL material in §C, §D3, §E1, §F and §G2–G3 is candidate testimony or single-source leakage and **must not be represented to the candidate as micro1 policy**." The doc's own header (line 5) promises "This document does not assume platform mechanics it cannot verify." Items 1, 2 and 4 of the list *are* verified, and item 2 is properly hedged ("Multiple candidates independently report") — items 3 and 5 are not.

**Corrected wording (header + tags):** change the header to "**Platform facts — verified vs candidate-reported** (grades per `micro1_platform_research.md`)" and tag: item 3 "(candidate-reported, not micro1 policy)", item 5 "(candidate-reported; the rephrase route is consensus advice, not a documented guarantee)", and the §0.2 note about typing-with-no-input-field "(one candidate report)".

### F-11 · data-analyst §6.1 — "in every join and aggregate" · IMPRECISE · **L**

> "**Nulls and blanks** — including the difference between `NULL`, empty string, `0`, and `"N/A"`. They behave differently in every join and aggregate."

**What's wrong:** "every" is an overstatement — `COUNT` ignores both `NULL` and `''` identically, and an inner equi-join treats `NULL = NULL` as false while `'' = ''` is true, so the *differences* are specific rather than universal. A pedantic interviewer can pick at it.

**Corrected wording:** "…They behave differently in joins and aggregates in ways that matter: `NULL` never matches `NULL` in an equi-join, `''` does, and both are ignored by `COUNT` — so a 'missing' count depends on which of the two you actually have."

### F-12 · data-analyst §5.2 — `COUNTIF` over 50,000 rows with no performance caveat · TECH-ERROR · **L**

> "Exact duplicates: `COUNTIF` on the key column, filter anything above 1…"

**What's wrong:** the question names 50,000 rows, and a full-range `COUNTIF` per row is quadratic (~2.5bn comparisons) — in Sheets it is genuinely slow, and an interviewer who asks "how long does that take?" gets an answer the doc has not prepared. Not wrong, incomplete.

**Corrected wording (append):** "On 50,000 rows I'd bound the `COUNTIF` range (or use a pivot / Remove Duplicates / Power Query) rather than run a full-column `COUNTIF`, which is quadratic — the answer is the same, the runtime isn't."

### F-13 · evaluator §4.1 — Axis 1 contradicts its own matrix · INTERNAL-CONTRADICTION · **H**

> "**Axis 1 — Reversibility.** Can this be undone cheaply? If yes, act. **If no, escalate.**"
> … matrix cell (Irreversible / high-impact × **Guideline covers it clearly**): "**Decide, but log it.**"

**What's wrong:** the axis text says irreversible ⇒ escalate, full stop. The matrix says irreversible + clearly covered ⇒ decide. Both are on the same screen, under a heading that says "memorise the two axes". In the interview, "Judging When to Step In" is the topic being tested — and if he recites the axis rule and then the matrix, he has given two different answers to the same question.

**Corrected wording (Axis 1):**
> "**Axis 1 — Reversibility.** Can this be undone cheaply? If yes, act. If no, act **only** where the guideline is explicit — and log it. Where it isn't explicit *and* it isn't undoable, escalate."

### F-14 · evaluator §4.1 — "Decide, then flag" contradicts three later sections · INTERNAL-CONTRADICTION · **H**

> matrix cell (Reversible × **Genuine edge case / not covered**): "**Decide, then flag.** Make the defensible call, note the gap so the guideline improves."

**What's wrong:** three other places in the same file say the opposite for exactly this case —
- §4.2 item 4 lists "**Genuine guideline gaps** — the case the rubric doesn't cover" under "**The categories where you always step in**";
- §5.1 "Ambiguity escalation": "Flag as not covered, state what you'd have scored and why, **escalate for the guideline owner**. Do not stretch a criterion.";
- §2.4 drill: "**I don't resolve it myself** — that's a judgement call above my authority."

A candidate who has memorised the matrix ("reversible + not covered = decide") and then answers the §5.1 question with "escalate" is contradicting himself inside one 20-minute interview.

**Corrected wording (matrix cell):**
> "**Decide the item, escalate the gap.** Score it as 'not covered', state what you'd have scored and why, and raise the gap to the guideline owner — the *item* is yours to call, the *rule* is not. Do not stretch a criterion to fit."

### F-15 · evaluator §4.1 — the confidence axis has no cell in the matrix · FRAMEWORK-GAP · **M**

> "**Axis 2 — Confidence and coverage.**" · matrix columns: "Guideline covers it clearly" / "Genuine edge case / not covered" · §4.2 item 6: "**Confidence below the threshold you'd defend** — if you wouldn't defend the call to a reviewer, escalate it rather than ship it."

**What's wrong:** the axis is named for two things and the matrix encodes only one of them. A case that is *clearly covered* but where his confidence is low reads as "**Decide**" in every cell of the matrix, while §4.2 item 6 says escalate. Coverage and confidence are independent, and only coverage is in the grid.

**Corrected wording (add under the matrix):**
> "**In every cell:** escalate if your confidence is below the threshold you'd defend (§4.2.6). Coverage decides *who owns the rule*; confidence decides *whether you should be the one applying it*. The matrix is not a licence to act on a call you couldn't defend to a reviewer."

### F-16 · evaluator §0 and §5.3 — single-source anecdote presented as micro1's own · UNSOURCED · **M**

§0 header: "**Platform facts that change how you prepare** — All verified in `micro1_platform_research.md`:" (same ANECDOTAL items as F-10: intro-seeding, no scroll-back, rephrase).
§5.3: "**micro1's own feedback email** flags *"how to score partial correctness"* as something candidates handle weakly."

**What's wrong:** the feedback email is graded **ANECDOTAL — one leaked email, reproduced by a candidate** in `micro1_platform_research.md` §E1 and source-table line 460, and the research file's closing line forbids representing §E1 as micro1 policy. The sibling doc handles this correctly ("micro1's post-interview feedback email — **reproduced by a candidate** and consistent with micro1's published question bank and its Cortex product language", data-analyst §0.1); this file does not.

**Corrected wording (§5.3):** "micro1's post-rejection feedback email — **reproduced by one candidate**, and consistent with micro1's published question bank and Cortex language — flags 'how to score partial correctness' as a gap." (Keep the advice; add the hedge.) And apply the F-10 header fix to §0.

### F-17 · all three files — the "Never say" lists are not equivalent, and none is complete · CONSISTENCY · **M**

Compared against `outreach_templates.md` §6 and `config/profile.md` rules 7 and 10:

| Forbidden claim (authority) | icici §9 | data-analyst §8 | evaluator §7 |
|---|---|---|---|
| Title above Data Analyst / people-management (profile 4–5) | ✅ | ✅ | ✅ |
| A number not in profile.md (profile 2/11) | ✅ | ✅ | ✅ |
| Independent projects as employer/client work (profile 9) | ✅ | ✅ | ✅ |
| BugAgents vendor / asset / repository / vulnerability class (profile 7) | ✅ | ✅ | ✅ |
| BugAgents "disclosed / accepted / paid" (profile 7) | ❌ | ❌ | ✅ (missing "resolved") |
| BugAgents "**resolved**" (profile 7, explicit) | ❌ | ❌ | ❌ |
| Production users / revenue / adoption (profile 10) | ❌ | ❌ | ❌ |
| "Peer-reviewed" / "published in a journal" (profile 13) | ✅ | ✅ (peer-reviewed only) | ✅ (peer-reviewed only) |
| Authoring the AgentSwarm papers (profile 13 / templates §6) | ❌ | ❌ | ❌ |
| "We" about solo work (interview_guide "one rule" #5) | §8 only | ✅ | ❌ |

**What's wrong:** each list is individually sensible, but they are three different documents' worth of guardrails for the same candidate, and the two prohibitions most likely to be blurted under pressure — "**resolved**" (the profile lists it explicitly alongside disclosed/accepted/paid) and **production users / revenue / adoption** (profile rule 10) — appear in **none** of them. Both are the kind of claim a candidate makes in an offhand "it's live and people use it" sentence.

**Corrected wording:** either make all three pocket-card lists the same seven bullets, or add one line to each: *"Full forbidden list: `outreach_templates.md` §6 — it binds here. It includes 'resolved' for BugAgents, any production-user/revenue/adoption claim, and claiming authorship of the AgentSwarm papers."*

---

## Domain definitions audit — `icici_lombard_interview_prep.md` §7.3 (current revision, 13 rows)

Verified term-by-term as a sceptical general-insurance interviewer would. This is a domain-knowledge audit: `irdai.gov.in` was unreachable in this session (recorded as 504 by the intel-researcher) and I could not fetch a primary IRDAI source. The regulator's identity and its statutory solvency-margin function are corroborated by Wikipedia's IRDAI article (<https://en.wikipedia.org/wiki/Insurance_Regulatory_and_Development_Authority>).

| Term | Verdict | Note |
|---|---|---|
| GWP / GDPI | **CORRECT** | GDPI = gross **direct** premium, excludes reinsurance assumed, gross of cession; it is indeed the headline Indian GI metric. The GWP/GDPI distinction is drawn correctly. |
| Loss ratio | **CORRECT but incomplete** | "Incurred claims ÷ premium earned" is right; should say **net** for the reported form (F-03). |
| Incurred Claims Ratio (ICR) | **CORRECT** | Net incurred claims over net earned premium; genuinely the term used in Indian GI disclosures. Good addition — it is what the interviewer will actually say. |
| Combined ratio | **CORRECT** | Loss + expense ratio; <100% underwriting profit, >100% underwriting loss, investment income as the offset. The parenthetical "(typically offset by investment income)" is the right nuance to carry. |
| IBNR | **CORRECT** | "Occurred but not yet notified" is the standard definition; "actuarial estimate, inputs must be auditable" is the right framing for this candidate. |
| Claims TAT | **CORRECT** | Registration→settlement; IRDAI does mandate settlement timelines, so "regulator-visible" is fair. |
| Persistency / renewal rate | **CORRECT** | Renewal rate is the GI analogue of life persistency; pairing the two terms is right, and "measured on premium or policy count" is accurate. |
| Fraud / leakage | **CORRECT** | Leakage as the broader category (process error, wrong tariff, duplicate settlement) with fraud as the deliberate subset is the accepted relationship. |
| IRDAI | **CORRECT** | Correctly expanded; "reporting, solvency and disclosure obligations flow from it" is accurate. |
| Solvency ratio | **CORRECT** | Available ÷ required solvency margin; capital adequacy, not profitability. The doc wisely does **not** quote the 1.5× minimum, so there is no number to be stale. |
| Motor OD / TP | **CORRECT** | OD vs TP right; TP is statutorily mandated, genuinely long-tail (bodily-injury development) and historically loss-making in India; "the split matters for reserving" is correct and is a good thing to say to an insurer. |
| Bancassurance / distribution mix | **CORRECT** | Bank partners, agents, brokers, direct; drives acquisition cost. |
| Ceding / reinsurance | **IMPRECISE** | The "therefore net loss ratios" step is wrong for proportional cessions — see **F-02**. |

**Prior-revision note (marked stale, not dropped):** in the earlier 405-line revision I read, §7.3 had 12 rows and defined GWP only as "total premium written before deductions", with no GDPI and no ICR. Those two gaps are **fixed in the current revision** — the Lead's rewrite is an improvement, and the only remaining defect is F-02.

---

## Technical claims audit

### Spreadsheet — `micro1_data_analyst_prep.md` §5 (current revision)

| Claim | Verdict |
|---|---|
| "Exact lookup: `XLOOKUP` (or `INDEX`+`MATCH`) — preferred over `VLOOKUP` because it doesn't break when columns move and it can search leftward" | **OK** — both advantages confirmed (Exceljet XLOOKUP: "can look up data to the right or to the left"; defaults to exact match). |
| "Approximate / banded lookup … requires sorted data" | **ERROR (F-06)** — true for `VLOOKUP` TRUE and for `XLOOKUP` binary search; false for `XLOOKUP` `match_mode` -1/1. |
| "`SUMIFS`, `COUNTIFS`, `AVERAGEIFS` … multiple criteria, and it doesn't need the data sorted" | **OK** — correct, and it is the right thing to say. |
| "`IFS` over nested `IF` for readability" | **OK** (Excel 2019+/Sheets). |
| "`IFNA` is better when you only want to trap 'not found' and still see real errors" | **OK** — `IFNA` traps only `#N/A`; `IFERROR` swallows every error class. Correct as stated. |
| "`TRIM`, `CLEAN`, `SUBSTITUTE`, `TEXTSPLIT`/`TEXTBEFORE`/`TEXTAFTER` — trailing spaces and non-printing characters are the most common cause…" | **PARTIAL ERROR (F-07)** — availability unstated (365-only; absent from Sheets), and `TRIM`/`CLEAN` do not remove `CHAR(160)`. |
| "Deduplication: `UNIQUE`, `COUNTIF`" | **OK**, with the performance caveat in F-12. |
| "Ranking / top-N: `LARGE`, `SMALL`, `RANK`" | **OK**. |
| "Dates: `EOMONTH`, `EDATE`, `DATEDIF`, `YEARFRAC`" | **OK** — `DATEDIF` is legacy/undocumented in Excel but functional in Excel and Sheets; fine to name. |
| Pivot tables / data validation / conditional formatting rows | **OK** — the "data validation is the cheapest data-quality control there is" framing is exactly right. |
| "Power Query — repeatable cleaning steps you can refresh" | **OK as a description, incomplete on availability (F-07)** — Excel/Power BI only. |
| §5.2 "`VLOOKUP` returns `#N/A`… `FALSE` for exact match, because the default approximate match silently returns a wrong-but-plausible answer" | **OK** — the 4th argument does default to `TRUE` (approximate); the advice is correct and the reasoning is the right one. |
| §5.2 layering answer (raw / cleaning / calculation / presentation, no manual edits to raw) | **OK**. |
| §5.2 Excel-vs-Sheets honesty block (added in the current revision) | **OK and important** — it is the correct posture; F-07 is the §5.1 table failing to follow it. |

### Data quality — `micro1_data_analyst_prep.md` §2.1/§2.2/§6

| Claim | Verdict |
|---|---|
| The six dimensions, in that order, are "the standard vocabulary of the field" | **OK** — completeness, accuracy, consistency, timeliness, validity, uniqueness is the standard DAMA core set. |
| "…because the cheap checks eliminate most of the problem before you spend effort on the expensive ones" | **ERROR (F-08)** — reconciliation (accuracy) is the expensive check and it is second. |
| Referential integrity filed under **Validity** | **OK / defensible** — widely done, though some frameworks separate an "Integrity" dimension. Not worth changing; if pushed, "referential integrity is a validity rule in my framework" is a fine answer. |
| Review vs validation definitions | **OK** — "review produces an opinion, validation produces a gate" is a good line and the definitions are standard. |
| §2.2's mapping of the agent to validation and Optum to review | **CONTRADICTION (F-09)**. |
| §6.1 error/edge-case checklist (10 categories) | **OK** — a genuinely strong checklist; joins/inner-join/fan-out, ties in top-N, row-level permissions and 0–1 vs 0–100 percentages are all real and correctly described. |
| §6.1 item 2 "they behave differently in every join and aggregate" | **IMPRECISE (F-11)**. |
| §6.3 "timestamps in UTC reported in IST move transactions across day and month boundaries" | **OK — and correct arithmetic**: IST is UTC+5:30, so a 20:00 UTC posting on 31 Jan lands on 1 Feb locally. |
| §6.3 "with a timestamp you silently lose everything after midnight on the 31st" | **OK** — correct behaviour of `BETWEEN '2026-01-01' AND '2026-01-31'` against a timestamp column. |
| §6.3 "six things" monthly-revenue answer (join, fan-out, boundaries, refunds, currency, duplicates, reconciliation) | **OK** — no technical error; the reconciliation closer is the right instinct. |
| §2.4 silent-failure story ("AI Safety track weight bug") | **OK** — traceable to `interview_guide.md` line 123 (weight of 0.6 applied as a multiplier capped the track below threshold → zero candidates). Correctly described as a JobAgents bug. |
| §4.4 review invariants / 8-8 guard | **OK** — matches `config/profile.md` lines 106–107 and `interview_guide.md` line 111. |

### Agent evaluation — `micro1_ai_agent_evaluator_prep.md` §4.1/§4.2/§5.1

| Claim | Verdict |
|---|---|
| §4.1 Axis 1 vs matrix | **CONTRADICTION (F-13)**. |
| §4.1 "Decide, then flag" vs §4.2.4 / §5.1 / §2.4 | **CONTRADICTION (F-14)**. |
| §4.1 Axis 2 "confidence and coverage" vs the matrix / §4.2.6 | **GAP (F-15)**. |
| §4.1 "the bar for acting alone goes up as reversibility goes down" | **OK** — the principle is sound and is the sentence worth memorising. |
| §4.2 escalation triggers (scope, irreversible, safety/legal/privacy, guideline gaps, conflicts of interest, low confidence, others' identity/terms) | **OK** — a genuinely good list; the "identity, account, or acceptance of terms that isn't yours" item is the one most evaluators miss. |
| §4.4 "90% right, ship or escalate?" | **OK** — "the question isn't how much is right, it's what kind of thing is wrong" is the right answer to that question. |
| §5.1 "Find the first divergence, not the final error" | **OK** — correct trace-evaluation method. |
| §5.1 rubric-writing: "independently checkable and binary or clearly banded" | **OK**. |
| §5.1 error taxonomy: capability / compliance / honesty | **OK** — and "honesty failures are the serious class" is defensible. |
| §5.1 tool-usage judgement | **OK**. |
| §5.2 first-principles fallback | **OK**. |
| §5.3 partial-credit answer ("Only if the rubric allows it… score per criterion, not per output") | **OK** — technically the right answer; the sourcing hedge is the only issue (F-16). |

---

## Ground-truth metric spot-check (all against `config/profile.md`)

Every count in the task's verification list appears with the correct value, or does not appear at all. **No mismatches.**

| Claim | profile.md | icici | data-analyst | evaluator |
|---|---|---|---|---|
| 18 ETL pipelines / 18 industry sectors | 41, 94 | ✅ | ✅ | ✅ |
| 10+ client dashboards | 47, 95 | ✅ | ✅ | — |
| 30+ analytical reports | 48, 96 | ✅ | ✅ | — |
| 3.5+ years | 22 | ✅ | ✅ | — |
| 9 years Optum | 22, 51 | ✅ | ✅ | — |
| 22,839 match scores / 155 above threshold | 101–102 | ✅ | — | ✅ (22,839) |
| 7,613 jobs / 5,854 distinct roles / 1,759 dupes / 10 sources | 98–100 | ✅ | — | — |
| 8/8 seeded fabrications | 106 | ✅ | ✅ | ✅ |
| 0 failures, every check fires (review invariants) | 107 | — | ✅ | — |
| 34 refused / 2 promoted (BugAgents) | 131–132 | ✅ | — | ✅ |
| 35/35 hash chains / 34 runs | 109–110 | ✅ | — | — |
| 1,441 turns / 1,553 commits / 330 turns / 100% CI | 80–81 | ✅ | — | — |
| 76.5% vs 25.5% (+51%) | 82 | ✅ | — | ✅ |
| 83.4% fitness / <4,000 words | 78–79 | ✅ | — | ✅ |
| 18,000+ / 59 colleges / 73 ranks / 90.6% | 84–86 | ✅ | — | — |
| pandas, FastAPI, PyTorch in Skills | 142 | ✅ (icici §8) | — | — |
| **Any of the 19 stale values** (7,533 · 5,784 · 1,864 · 22,647 · 274 · 9 sources · 32 runs · 32/32 · 3,156 · 53 turns · 182 reports · 158 engines · 209 artifacts) | 70–72 | ❌ none | ❌ none | ❌ none |

**Publication/disclosure/seniority checks:** Paper 1 = "Zenodo preprint — not peer-reviewed" (icici §6.2, evaluator §8) ✅ · Paper 2 = "not submitted" ✅ · agent authorship disclaimed ✅ · BugAgents = "nothing has been submitted to any program" ✅ · titles "Data Analyst at both employers" ✅ · independent projects labelled as such in all three ✅ · no production-user/revenue/adoption claim anywhere ✅ · pocket-card "Say" bullets in all three are fully traceable ✅ · the two micro1 invitation quotes and topic lists are **verbatim-accurate** against the screenshots ✅.

---

## Claims I could NOT verify either way

1. **`$150k+` (icici §2.4)** — I could not verify it *or* find any source for it. It is not in `profile.md`, `interview_guide.md`, `outreach_templates.md`, or any other repo file. Only the candidate can settle this. **This is the single most consequential unverified item in the three docs** (F-01).
2. **Implementation details of Black Piano work that `profile.md` does not record** — e.g. "Eighteen sectors is not eighteen bespoke systems — it's one pipeline shape parameterised per sector" (icici §5.1), "the reference table handles the overwhelming majority" (icici §4.2), and "the auto-exported Sheets pipelines exist so the model reads real numbers" (icici §5.3). These are plausible and internally consistent, but there is no Black Piano code in this workspace to check against, and `profile.md` records outcomes, not architecture. They are safe to say **only if true**, because each invites a deep follow-up ("show me the parameterisation").
3. **ICICI Lombard's actual data platform** — the claim that there is "no evidence of GCP, BigQuery or Looker anywhere at the company" is, per the research file itself, *absence of evidence in reachable sources*, and the primary documents (annual report, Digital Day 2026 deck) were PDFs the researcher could not parse. The prep doc states this caveat correctly in §2.5; I could not improve on it. Do not let it harden into "they don't have GCP".
4. **The ₹11.2 L/yr aggregator figure and ICICI Lombard's real band** — login-gated aggregator, internally inconsistent (also shows 16.5), graded WEAK. Unverifiable from here.
5. **Whether "Swarnim Vaidya" works at ICICI Lombard** — not verifiable without LinkedIn auth; both the research file and the prep doc correctly mark it unverified and tell him to check.
6. **micro1 platform mechanics that the research file itself grades UNVERIFIED/ANECDOTAL** — exact per-question time limits and question counts, retake policy, whether a written/task portion applies to his two interviews, whether either is proctored, whether typing scores differently, and India-specific rate adjustment. The prep docs mostly avoid asserting these; where they don't, see F-10/F-16.
7. **Spreadsheet-function availability statements (F-07)** — `TEXTSPLIT`/`TEXTBEFORE`/`TEXTAFTER` being 365-only and absent from Sheets, and Power Query being Excel/Power BI-only, are stated from product knowledge. I attempted Microsoft's own documentation pages; they return only JS navigation chrome in this environment, so I could not attach a citation. **The XLOOKUP finding (F-06), by contrast, is externally verified** (Exceljet).
8. **Insurance glossary against a primary IRDAI source** — `irdai.gov.in` was unreachable (504, recorded by the intel-researcher). The §7.3 audit above is domain-knowledge-based; the definitions are standard, and I found no hard error — only the two precisions in F-02/F-03.
9. **The exact revenue/settlement-timeline specifics behind "Claims TAT … a regulator-visible one"** — true in substance (IRDAI mandates claim-settlement timelines); I did not verify the specific regulation number and the doc does not cite one, so nothing is at risk.

## Minor, non-blocking (fix if you are already in the file)

- **icici §0.4** — "Four risks to price in early — **all sourced in §2**", but the first bullet (recruiter identity) points to **§1.3**. Change to "all sourced below".
- **icici §0.4 / §2.4** — the fourth risk bullet says "~3.5 years in data against 12.5 years total"; 3.5 + 9 = 12.5 ✅ correct, and consistent with the research file. No action.
- **evaluator §5.0** — "your interview topics map onto them **one-to-one**": the mapping table pairs "Monitor reliability" with "Hands-On Use of AI Tools" and "Expert training data" with "Following Detailed Instructions Exactly", which are the two weakest pairings, and one of the interview's four topics ("Custom questions defined for the job") is not a Cortex step at all. Soften to "map onto them closely" — the substance (micro1's own vocabulary is the register to answer in) is right.
- **evaluator §7 / data-analyst §0.2** — both correctly hedge candidate testimony; no action. Noted only because the same material is asserted flatly in evaluator §0 and §5.3 (F-16).

## What I would fix first (ordered)

1. **F-06** — the XLOOKUP sorting error. One line, in the one section that is directly examined.
2. **F-13 + F-14** — the §4.1 matrix. Two cells and one axis sentence; otherwise the highest-signal topic in the evaluator interview contains a self-contradiction he will recite.
3. **F-01** — remove or source `$150k+`.
4. **F-07** — platform-tag the §5.1 function table (and add the `CHAR(160)` fix).
5. **F-10 + F-16** — retitle the two micro1 "platform facts" headers and hedge the leaked-email claim, so the docs keep the sourcing standard they set for themselves.
6. **F-08, F-09, F-15, F-17** — the rationale, the inverted review/validation mapping, the confidence gap, and the "Never say" lists.
7. **F-02, F-03, F-04, F-05, F-11, F-12** — polish.

---

# Post-fix delta — re-verification of the Lead's edits

**Date:** 2026-10-12, 10:15–10:30 · **Scope:** changed sections only, per the Lead's request. The original 17 findings remain as written above; this section records their status against the edited files.

## Revisions re-verified (SHA256, current on disk)

| File | Lines | SHA256 (first 16) | Status |
|---|---|---|---|
| `docs/icici_lombard_interview_prep.md` | 477 | `B89362FB69707987` | edited (was 468) |
| `docs/micro1_data_analyst_prep.md` | 430 | `9F097E403E5854E2` | edited (was 416) |
| `docs/micro1_ai_agent_evaluator_prep.md` | 391 | `21E33B03BB61E382` | edited (was 382) |
| `docs/linkedin_blackpiano_rewrite.md` | 177 | `32D15CFAE6AB99FA` | **new — outside my original scope; reviewed for awareness only** |

## Status of the 17 findings

| Finding | Status | Evidence in the edited files |
|---|---|---|
| F-01 `$150k+` unsourced | **CLOSED as to the number** — one new sub-issue, see NEW-01 | icici §2.4 line 157: figure removed, explicit "no dollar figure is quoted here on purpose… it is not in `config/profile.md`" |
| F-02 ceding → net loss ratio | **CLOSED** | icici §7.3 line 405 — proportional cession stated correctly, plus non-proportional cover / ceding commission / line mix, plus the "reinsurance lowers our loss ratio" tell |
| F-03 loss ratio / ICR gross vs net | **CLOSED** | icici lines 394–395 — **net** stated in both rows, "expect 'net or gross?' as the follow-up" |
| F-04 ₹11.2 L vs §9 | **CLOSED** | icici line 172 — "never repeat this figure to the recruiter or in the interview (§9)" + the 16.5 internal inconsistency; line 462 repeats the prohibition in the pocket card |
| F-05 CTO dates | **CLOSED** | icici line 20 — AI since 2021, fraud detection since at least 2024 |
| F-06 XLOOKUP sorted-data error | **CLOSED** | data-analyst line 288 — correct in full (see (b) below) |
| F-07 TEXTSPLIT / Power Query / CHAR(160) | **CLOSED** | data-analyst lines 287, 292, 299 + the "name the platform with the function" rule at line 322 (one residual nit, see (b)) |
| F-08 DQ order rationale | **CLOSED** | data-analyst lines 125–127 — "standard checklist, then triage by cost", with the reconciliation-is-expensive note and the exact follow-up it defuses |
| F-09 review/validation inversion | **CLOSED** | data-analyst lines 136–141 — Optum is the gate (validation), the agent is detection and recovery, "prevention is the audit habit, recovery is the agent" |
| F-10 "All verified" over ANECDOTAL items | **PARTIAL** | §0 list correctly re-graded, but four later instances remain flat — see (c) |
| F-11 NULL/blank overstatement | **CLOSED** | data-analyst line 333 — NULL never matches NULL, `''` does, both ignored by `COUNT`, and `0`/`"N/A"` pass a null check |
| F-12 COUNTIF quadratic | **CLOSED** | data-analyst lines 293 and 304 — caveat added in both the table and the drill |
| F-13 Axis 1 vs matrix | **CLOSED** | evaluator line 174 vs matrix line 181 — they now agree |
| F-14 "Decide, then flag" | **CLOSED** | evaluator line 180 + line 189 + §5.1 line 266 + §2.4 line 110 — all four now say the same thing |
| F-15 confidence has no cell | **CLOSED** | evaluator line 176 (axis split) + line 183 ("in every cell" rule) |
| F-16 leaked-email claim | **CLOSED** | evaluator line 279 — "reproduced by one candidate"; §0 items tagged |
| F-17 "Never say" lists | **CLOSED** | all three now carry "resolved", production users/revenue/adoption, paper authorship, and the `outreach_templates.md` §6 pointer (icici 455–465, data-analyst 417–424, evaluator 377–385) |

**15 closed · 1 partial · 0 still open.**

## (a) F-13/F-14/F-15 — resolved, not relocated

The four places that previously disagreed now agree, and I checked each pairing rather than the matrix alone:

- **Axis 1 ↔ matrix:** line 174 ("If no, act **only** where the guideline is explicit — and log it. Where it isn't explicit *and* it isn't undoable, escalate") is exactly the matrix's two irreversible cells (line 181: "Decide, but log it" / "Escalate").
- **Matrix ↔ §4.2 item 4 ↔ §5.1 ↔ §2.4:** line 180 ("Decide the item, escalate the gap… The *item* is yours to call; the *rule* is not"), line 189 (the spoken item/rule distinction), §5.1 line 266 ("escalate the **gap**, not the item"), and §2.4 line 110 ("I don't resolve it myself… I'd apply the more specific instruction if one is clearly more specific… and raise the conflict") are now one consistent position. §4.2 item 4 ("Genuine guideline gaps") sits under "categories where you always step in", which is consistent with escalating the gap.
- **Confidence:** line 176 splits coverage from confidence and line 183 supplies the missing rule ("escalate if your confidence is below the threshold you'd defend (§4.2 item 6)"), which is what §4.2 item 6 needed.

*Optional nit (not a finding):* §4.2 item 4 could carry "(the gap, not the item — §4.1)". Given the four agreeing statements it no longer contradicts anything, but under 20-minute pressure the gloss "the case the rubric doesn't cover" still reads as the item.

## (b) F-06/F-07 — now technically correct

- **Line 288 is right in every clause:** `match_mode` -1 = exact or next smaller, 1 = exact or next larger; XLOOKUP's approximate match does not need sorted data; `VLOOKUP` with `TRUE` requires the first column ascending; sorting is required only for XLOOKUP binary search (`search_mode` 2 / -2). That is the same structure as the externally verified reference I cited in F-06.
- **Line 287** correctly adds "Excel 2021+/365 and in Sheets" for XLOOKUP.
- **Line 292** is right on both counts: `TRIM` removes ASCII space only, `CLEAN` strips chars 0–31, `CHAR(160)` survives both, and the fix is `SUBSTITUTE(x,CHAR(160)," ")`; `TEXTSPLIT`/`TEXTBEFORE`/`TEXTAFTER` are flagged Excel 365 only, not Excel 2019/2021 and not Sheets, with `SPLIT`/`REGEXEXTRACT` given as the Sheets equivalents.
- **Line 299** correctly moves Power Query out of the Sheets path and names the Sheets equivalents.
- **Line 322** adds the rule that makes the whole section safe.

*Residual nit (not a finding):* the §5.2 drill at line 310 still says "Use Power Query or formulas for the cleaning…" — in a Sheets-based interview that should read "a query sheet or Apps Script (Sheets) / Power Query (Excel)", otherwise the drill names the tool the row above it just flagged as unavailable to him.

## (c) §0 grading tags — match `micro1_platform_research.md` item by item

| Doc | Item | Tag now used | Research grade | Verdict |
|---|---|---|---|---|
| data-analyst | 1 Zara / real-time verdict | VERIFIED | A2, B2 VERIFIED | ✅ |
| data-analyst | 2 never go silent | CANDIDATE-REPORTED | §C2 ANECDOTAL | ✅ |
| data-analyst | 3 free mock interview | VERIFIED | §1 line 37 VERIFIED | ✅ |
| data-analyst | 4 certification gate | VERIFIED | A2 VERIFIED | ✅ |
| data-analyst | 5 rephrase / no scroll-back | CANDIDATE-REPORTED | §B3 ANECDOTAL | ✅ |
| evaluator | 1 Zara / real-time verdict | VERIFIED | A2, B2 VERIFIED | ✅ |
| evaluator | 2 never go silent | CANDIDATE-REPORTED | §C2 ANECDOTAL | ✅ |
| evaluator | 3 free mock interview | VERIFIED | §1 line 37 VERIFIED | ✅ |
| evaluator | 4 pre-interview screen | VERIFIED | staff reply, source table line 458 ("near-official") | ✅ defensible — the research legend counts official staff posts as VERIFIED, though this is one notch weaker than a website/legal statement |
| evaluator | 5 seed the intro | CANDIDATE-REPORTED | §B3 ANECDOTAL | ✅ |
| evaluator | 6 rephrase / no scroll-back | CANDIDATE-REPORTED | §B3 ANECDOTAL | ✅ |
| evaluator | 7 certification gate + 30 days | VERIFIED | A2 VERIFIED (micro1's own 30-day statement) | ✅ |

**F-10 is PARTIAL, not closed:** the tagging was applied to the §0 lists, but the same candidate-reported mechanics are still asserted flat in four later places in the data-analyst doc —
- line 62 "Zara generates follow-ups from the *end* of your introduction" (§0.2 item 3),
- line 66 "the platform has a known failure where it asks you to type when no input field is visible" (one candidate report in the research file),
- line 99 "Zara reads a pause as *'answer finished'* and moves on" (§1.3 trap 1),
- line 106 "It is permitted… you cannot scroll back through the transcript".

This now contradicts the doc's own line 22 instruction ("Do not treat a candidate-reported item as platform policy"). The practical advice is identical either way, so this is low severity — but it is the exact standard the file sets for itself. Cheapest fix: one "(candidate-reported — §0)" tag on line 62, one on line 66, and a single "(candidate-reported)" parenthetical at the head of §1.3's trap list. The evaluator doc has **no** such residue: all three instances there (lines 28, 31, 32) are tagged.

## (d) F-01 rewrite — the number is gone; one new claim

The `$150k+` figure is removed and replaced with an explicit statement that no figure is quoted because none is in `config/profile.md`, plus an instruction to confirm his own walk-away number. That is exactly what F-01 asked for. **But the replacement sentence introduces one claim that is not traceable to the ground truth — see NEW-01.**

## (e) Cross-references — clean, with one exception

- **evaluator §7/§8 renumbering broke nothing.** The only internal section references in the file are line 183 ("§4.2 item 6"), line 382 ("§3.3") and line 383 (a cross-file pointer) — all valid. No reference to "§7" meaning the pocket card survives anywhere.
- **Cross-file references checked:** `micro1_data_analyst_prep.md` line 145 → icici §4 (valid); `micro1_ai_agent_evaluator_prep.md` line 383 → data-analyst §5 (valid); icici line 172 → "(§9)" (valid, pocket card is still §9). The companion-file lines at the foot of each doc are all valid.
- **Exception:** the new LinkedIn doc skips a section number — see NEW-02.
- **Unchanged minor from the first pass:** icici line 14 still reads "Four risks to price in early — **all sourced in §2**" while the first bullet points to **§1.3**. Cosmetic.

## NEW findings introduced by the edits

**NEW-01 · icici §2.4 line 157 · UNSOURCED (low).** The rewrite replaces the unsourced dollar figure with "Your own recorded position is remote-first **and USD-denominated**." "Remote-first" is supportable (`config/profile.md` line 25: "Remote-global"; research §E.3: "remote, serving US/UK clients"). **"USD-denominated" is not in `profile.md`** — it is an inference in `icici_lombard_research.md` §E.3 drawn from Black Piano's client geography (profile lines 32–34 say the company "hires India-based talent to serve its US/UK clients", which says nothing about the currency he is paid in). If his package is INR-linked, the "these two positions may simply not overlap" argument in §2.4 is weaker than stated. *Fix:* "Your own recorded position is remote-first (profile: 'Remote-global'). If your package is USD-linked, say so — the mismatch argument is strongest in that case; if it is INR-denominated, the gap is about band, not currency."

**NEW-02 · `docs/linkedin_blackpiano_rewrite.md` · numbering gap (low).** The file has §1, §2, §4, §5, §6, §7 — **there is no §3**, and nothing references one. Either renumber or add the missing heading. Cosmetic, but the Lead asked to be told about numbering breakage.

**NEW-03 · `docs/linkedin_blackpiano_rewrite.md` §1/§2 · the template-leakage class is wider than the two bullets caught (medium).** The doc correctly finds the 60% and "4 enterprise clients" on LinkedIn and traces them to `config/profile.example.md` lines 42–43 (I verified both, plus the file's role as a template). But the same file contains at least two more divergences from the canonical profile, of exactly the kind that would have leaked the same way:
- line 37: the title is "**Data Analyst / AI Systems**" — the canonical profile (lines 32–34) says the title is **Data Analyst** at both employers and "do not inflate it";
- line 48: "automated BigQuery access across **15+ enterprise dashboards**" — canonical is **10+ client dashboards**, and "enterprise dashboards" is the specific wording `outreach_templates.md` §6 lists under "Never write" as superseded.

The provided screenshot (`assets/linkedin_blackpiano_current.png`) shows only the Black Piano section and the first two skills, so **the Pi Software section is unchecked**. Since the doc's own checklist item is "open the profile in a logged-out browser and read it once", extend that pass to the Pi Software section and the title line, and check for "15+", "enterprise dashboards", and any "/ AI Systems" title. This is the same defect class the doc was written to fix, one section further down.

**NEW-04 · `docs/linkedin_blackpiano_rewrite.md` §5 line 135 · inaccurate and incomplete (low).** "Your screenshot shows '+6 skills' truncated, so **I can't see what's currently listed**" — the screenshot does show the first two: "Python (Programming Language), Data Engineering and +6 skills". That matters because **"Data Engineering" is not in `config/profile.md`'s Skills list** (the Data category has BigQuery, Looker Studio, Tableau, ETL Orchestration, Data Modeling, Data Quality & Validation, Data Pipeline Maintenance, BigQuery Notebook, Scheduled Queries, Apps Script, SQLite). §5 tells him which skills to add and what not to add, but says nothing about the role-label skill already on his profile. *Fix:* state what the screenshot shows and decide it explicitly — either keep it (it is a role label, not a held title, so the title rule is not breached) or replace it with the verified `ETL Orchestration` / `Data Pipelines`.

**NEW-05 · `docs/linkedin_blackpiano_rewrite.md` §2 bullets 3 and 5 · OVERCLAIM relative to the canonical wording (medium-low).** Both are disclosed in the doc as deliberate reframes, but the published text is what a recruiter reads:
- bullet 3 ends "**replacing a recurring manual analysis step**" where `config/profile.md` line 40 says "**reduced client manual analysis time**". "Replacing" asserts the step is gone; "reduced" is what he is trained to defend (data-analyst §5.2 says "reduced client manual analysis time" is the verified phrasing, and §6.4 trains him to answer "I don't have a measured figure"). *Fix:* "…auto-published to a deployed client-facing website, **reducing a recurring manual analysis step**."
- bullet 5 upgrades "**Worked on** various industry reports (Black Friday, Christmas, sales) and ad-hoc dashboards" (line 37) into "**Automated** recurring industry reporting… **replacing manual refresh work with scheduled pipelines**". That attributes automation to specific reports the canonical profile does not. *Fix:* keep the canonical verb, or confirm before publishing that those reports are actually on a schedule.

**NEW-06 · data-analyst §5.2 line 310 · residual (low).** Folded into (b) above: the drill still names Power Query as the cleaning tool.

## What the edits did not break

- No stale value, overclaim, or misattribution was introduced anywhere in the three prep docs — I re-checked the metric table, the project-labelling sentences and the publication/disclosure claims in the changed regions.
- The two micro1 invitation quotes and topic lists are untouched and still verbatim-accurate.
- All three pocket-card "Say" lists remain fully traceable; the "Never say" lists are now equivalent in coverage.
- The glossary gained no new errors; the ceding row's added detail is correct.

---

# Post-fix delta 2 — final spot-check (2026-10-12, 10:20–10:25)

**Revisions verified:** icici 477/`D03B8E90A93A8052` · data-analyst 432/`800C6988F2BB6CF6` · evaluator 391/`21E33B03BB61E382` (untouched this round) · linkedin 213/`47754A7A57D4E96D`.

## Residual fixes — 4 of 4 CLOSED

| Item | Status | Evidence |
|---|---|---|
| F-10 candidate-reported tags | **CLOSED** | data-analyst line 62 `*(Candidate-reported.)*` + "reportedly"; line 66 `*(candidate-reported)*`; line 99 grading note covering traps 1 and 6; line 101 `*(Candidate-reported.)*` + "reportedly"; line 108 hedged ("Candidates report it as permitted… micro1 does not publish either as a guarantee"). Every candidate-reported mechanic in the file now carries a tag. |
| §5.2 Power Query nit | **CLOSED** | line 312 — "in Sheets that's a query sheet or an Apps Script job, in Excel it's Power Query". |
| icici line 14 "all sourced in §2" | **CLOSED** | line 14 — "all sourced below and in `icici_lombard_research.md`". |
| NEW-01 "USD-denominated" | **CLOSED** | icici line 157 — remote-first with the profile's own quote, plus "If your package is USD-linked, say so… If it is INR-denominated, then the gap is about the band, not the currency." No new unsourced claim; "remote-global baseline" is the profile's own word. |

## Skill-verbatim check

`ETL Orchestration`, `Data Pipeline Maintenance` and `Data Modeling` are all **verbatim** in `config/profile.md` line 143, alongside `BigQuery`, `Looker Studio`, `Tableau`, `Data Quality & Validation`, `Google Apps Script`, `SQLite`. The pinned trio — **ETL Orchestration / Python / SQL** — is verbatim (lines 143 and 142). The Lead's self-caught error ("Data Pipelines" is not canonical) is correctly fixed, and §5 now explains the substitution rule explicitly (line 168).

## LinkedIn doc — numbers clean, four skill entries still non-verbatim

**Numbers: clean.** Every figure in the publishable text is canonical (18 pipelines / 18 sectors, 10+ client dashboards, 30+ reports, nine years, Mar 2026–Present) or is explicitly presented as a claim being removed (60%, "4 enterprise clients", "15+ enterprise dashboards"). "Three years at Pi Software Solutions" is derived from the canonical dates (Mar 2023 – Feb 2026 = 35 months) and is acceptable rounding. "Up to 50 skills" is a LinkedIn platform fact, not a claim about him. **No number is recommended that is not in `config/profile.md`.**

**Skills: NOT fully closed.** The §5 list headed "Then, from your verified skill list only" (line 179) still contains four entries that are not verbatim canonical:

| Entry | Canonical position |
|---|---|
| `Data Analysis` | **not in the Skills list at all** — it is the job title's domain, not a listed skill |
| `Data Quality` | canonical is the single entry `Data Quality & Validation` (line 143) |
| `Data Validation` | same — the canonical entry is combined |
| `Multi-Agent Systems` | canonical is `Multi-Agent Swarms` (line 139) |

This is the same class of issue the Lead just corrected for "Data Engineering"/"Data Pipelines", applied one level further down. It is low severity — all four describe real work and none claims a tool he has not used — but it is inconsistent with the rule the doc states at line 121 ("the strict rule bites on the Skills section… every entry should be traceable to the canonical list"). *Fix:* merge `Data Quality` + `Data Validation` into `Data Quality & Validation`, rename `Multi-Agent Systems` to `Multi-Agent Swarms`, and either drop `Data Analysis` or replace it with `Data Pipeline Maintenance`. (`Large Language Models (LLM)`, `Fine-Tuning`, `Agent Evaluation`, `Model Context Protocol (MCP)` and `Google Cloud Platform (GCP)` are acceptable — they are the canonical category header or a faithful expansion/substring of canonical entries.)

## New leftovers from this round's edits (4, all low, all in the LinkedIn doc)

1. **Line 97 — stale text.** "the 60% is gone (replaced with **"replacing a recurring manual analysis step"** — true, and unfalsifiable in the good sense)" — the bullet (line 71) and the explanation (line 95) both now say **"reducing"**. Line 97 contradicts both. *Fix:* "…replaced with 'reducing a recurring manual analysis step'…".
2. **Line 187 — broken cross-reference.** "Publishing **§2** makes your profile and your interview script agree" — §2 is now the Pi Software defect section; the publishable section is **§3**. *Fix:* "Publishing §3…".
3. **Line 8 — incomplete reference.** "Every number below is either already in the canonical profile or flagged in **§1** for your decision" — the "15+ enterprise dashboards" figure is flagged in **§2**. *Fix:* "…flagged in §1–§2 for your decision."
4. **Line 89 — table gloss overstates the softened bullet.** The row reads "**5. Automated reporting** | *The unglamorous proof.* Recurring reports automated is exactly what an insurer's MIS team needs…", while bullet 5 was deliberately softened to "Worked on recurring industry reports… **automating the refresh where the cadence allowed**". *Fix:* relabel to "5. Recurring reporting" and "Recurring reports automated **where the cadence allowed**…", so the rationale table matches the bullet he will publish.

## Closing position

The three prep docs are **PASS** as of these revisions: every finding from the first pass and the first delta is closed, and no stale value, overclaim or misattribution survives in them. The only remaining defects are the four cosmetic leftovers and the four non-verbatim skill labels listed above, all in `docs/linkedin_blackpiano_rewrite.md`, which was outside my original scope and which the Lead can settle in one edit.
