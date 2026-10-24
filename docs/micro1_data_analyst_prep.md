# micro1 — "Data Analyst" AI Interview Prep (~43 minutes)

> **Source of truth for the format:** the invitation screenshot, preserved at [assets/micro1_data_analyst_43min.png](assets/micro1_data_analyst_43min.png).
> **Source of truth for every fact about you:** [../config/profile.md](../config/profile.md). If a number is not in that file, it does not get said out loud.
> **Platform context:** see [micro1_platform_research.md](micro1_platform_research.md) for what is verified about micro1 versus what is only candidate anecdote. This document does not assume platform mechanics it cannot verify.

---

## §0 — What this interview actually is

The invitation says, verbatim:

> *"Please note that this interview will take ~43 minutes with each question having a limited time for a response. You will answer by speaking, or typing. Ensure you're in a quiet spot with a stable internet connection. This interview will be recorded and available in your profile link."*

> *"You will be interviewed on these topics:"*
> - Data quality review & QA validation
> - Judgment under ambiguity & documentation of rationale
> - Rubric-based evaluation & guideline adherence
> - Spreadsheet proficiency (baseline)
> - Error & Edge-Case Detection

**Before anything else — the platform facts that change how you prepare.** Grades below are per [micro1_platform_research.md](micro1_platform_research.md), which distinguishes micro1's own published statements from candidate testimony. **Do not treat a candidate-reported item as platform policy** — prepare for it, but don't state it as fact if asked.

1. **VERIFIED — the interviewer is a voice AI called Zara. There is no human to read the room.** micro1 states plainly that it evaluates *"communication skills, logical reasoning, and role-specific skills"* and gives *"a real-time result indicating whether you meet micro1's global certification criteria."* You may get a verdict the moment you finish. **Prepare for a machine-readable answer structure, not for rapport.**
2. **CANDIDATE-REPORTED — never go silent.** Multiple candidates independently report that a pause is read as "answer finished." If you need to think, *say so out loud* — "let me think about that for a moment." This is the single highest-value behavioural change in this document, and it costs you nothing even if the report is wrong.
3. **VERIFIED — rehearse on the real product first, and it is free.** micro1 publishes mock interviews at `interview.micro1.ai/mock-interview` and a prep library at `micro1.ai/interview-prep`. Candidates who did the mock two or three times report it being the thing that de-risked the format. **Do this before the real one.**
4. **VERIFIED — this is a certification gate, not a job interview.** micro1 says: *"Certification does not guarantee immediate placement."* Passing puts you in a vetted pool; a client hiring manager reviews after. Treat a pass as *eligibility*, and keep your other applications running in parallel.
5. **CANDIDATE-REPORTED — you can ask Zara to rephrase.** Candidates report this is permitted and is the main recovery mechanism; micro1 does not publish it as a guarantee. The same reports say the transcript is live on screen and you **cannot scroll back** to re-read a question. Either way the advice is identical: **if you miss part of a question, ask rather than guess.**

**Four more things to internalise:**

6. **It is timed per question.** This is not a conversation where you can think out loud for 90 seconds and find your footing. A limited response window rewards a *pre-loaded structure*. Every answer in this document is written to be delivered in 60–120 seconds with a fixed shape: **answer first, reasoning second, caveat third.**
7. **You may speak or type.** Choose per question — §1.2.
8. **Assume it is transcribed and scored by someone who was not in the room.** No context you don't state, no references to things "as I mentioned earlier" without restating them.
9. **The five topics are not five subjects — they are one competency stack.** Read them together and a single thesis appears: *this role is about being a reliable, auditable judge of data and of AI output.* Data quality is the domain. Rubrics and rationale are the method. Ambiguity and edge cases are the hard part. Spreadsheets are the baseline tool.

**This is a data-quality-and-evaluation role, not a dashboard-building role.** Prepare as an *evaluator who can also build*, not as a builder who can also check.

### 0.1 The vocabulary micro1's own scoring language rewards

micro1's post-interview feedback email — reproduced by a candidate and consistent with micro1's published question bank and its Cortex product language — praises *"rubric-driven assessment, consistently mapping criteria and documenting rationale for each decision"*, *"factuality and safety as non-negotiable"*, *"awareness of different severity levels"*, and *"risk-based thinking."* It names as gaps *"a consistent, scalable severity taxonomy"*, *"calibration sets or inter-rater reliability"*, and *"how to score partial correctness."*

**These are concepts you already own from your own projects — you may just not be using the words.** Use them explicitly:

| Phrase to use | What it means in this interview |
|---|---|
| **"rubric adherence"** | Applying the written criteria literally, in their words, without substituting your own framework. |
| **"documenting rationale for each decision"** | Per-criterion: what you observed, why it meets or fails, and what would change your mind. |
| **"severity taxonomy"** | A named, ordered scale for how bad a defect is — and why this level and not the one above or below. |
| **"inter-rater reliability" / "calibration"** | How you stay consistent across a long batch, and consistent with other evaluators. |
| **"partial correctness"** | How you score something that is half right. Most real rubrics are not binary — say how you'd handle it. |
| **"intent alignment" / "factual accuracy" / "hallucination avoidance"** | The three axes of evaluating AI output. |
| **"edge-case test set"** | A deliberate set of boundary cases used to check whether a rule actually fires. |
| **"what's wrong, why it's wrong, and what to do next"** | The shape of actionable feedback. |

**Say these words.** They are not jargon for its own sake — micro1's own feedback language is built from them, and the topics on your invitation track its published question bank.

### 0.2 Five things to do before you click start

1. **Run the official mock interview two or three times.** `interview.micro1.ai/mock-interview`, plus the prep library at `micro1.ai/interview-prep`. It is the same application as the real thing and it is free. Candidates consistently report this as the single thing that de-risked the format. **Do this first — before reading the rest of this document twice.**
2. **Read the pre-interview screen carefully.** micro1 staff confirm it states *"skills assessed, duration, etc."* before you begin, and that whether a **written or task portion** is included is **role-specific**. This is the one free thing that resolves the biggest format unknown: whether your 43 minutes includes an interactive spreadsheet task alongside the conversation.
3. **Seed your own intro deliberately.** *(Candidate-reported.)* Zara reportedly generates follow-ups from the *end* of your introduction. So end the intro on the topic you want drilled — the data-quality agent and the pipelines, in that order. Even if the mechanism differs, ending on your strongest material costs nothing.
4. **Practise saying the answer shape out loud until it's automatic:** *"criterion applied → evidence observed → severity call → what would change my mind."* That sentence is the spine of most answers in this interview.
5. **Check your setup.** Wired connection if you can, quiet room, camera and mic tested, and **do not refresh the page** (stated on the invitation). If Zara freezes or stalls, official guidance is Chrome incognito or Firefox Private — multiple candidates report Chrome hanging and Firefox working. Know that fallback before you need it.

**On the day, if something goes wrong:** *(candidate-reported)* the platform can ask you to type when no input field is visible. If that happens, **say so out loud and ask for a rephrase or an alternative** rather than burning the timer in silence. The advice holds whether or not the failure recurs.

---

## §1 — How to play a timed AI interview

### 1.1 The answer template — use it for every question

| Beat | Time | What it does |
|---|---|---|
| **1. Direct answer** | 5–10s | Answer the question that was asked, first. Never build up to it. |
| **2. The criteria you applied** | 20–30s | *"I checked it against three things: completeness, consistency with the source, and whether the change was documented."* This is what "rubric-based" and "documentation of rationale" are testing. |
| **3. The concrete example** | 30–50s | One real project. Black Piano work first — it is employer work and it matches the topics. |
| **4. The edge case or limitation** | 15–25s | What would break it, what you did not cover. This is where you separate from the pile. |

**Why this shape:** it maps directly onto the scoring topics. Beats 2 and 4 are the ones most candidates skip, and they are the ones this interview says it is measuring.

### 1.2 Speak or type — decide per question, not once

| Use **speaking** for | Use **typing** for |
|---|---|
| Anything with a story or a trade-off ("tell me about a time…", "how would you handle…") | Anything with a **defined, listable** answer (a formula, a checklist, a sequence of validation steps) |
| Judgment calls, ambiguity, rationale — tone carries confidence | Spreadsheet functions, exact syntax, step-by-step validation logic |
| Anything where you want to show *how you think* | Anything where precision matters more than delivery |

**Rules for speaking:** say numbers slowly. Land the number, then pause. A mumbled figure invites doubt; a paused one reads as precision.

**Rules for typing:** short sentences. Bullets. No walls of text — a reader scanning a transcript rewards structure.

**Either way:** finish inside the window. An answer cut off mid-sentence loses beat 4 entirely, which is the beat that scores.

### 1.3 The six traps in this specific format

> **Grading note for traps 1 and 6 below:** the pause mechanic and the no-scroll-back transcript are **candidate-reported**, not micro1 policy. The advice is identical either way — narrate your thinking, and ask for a rephrase rather than guessing — so follow it regardless.

1. **Going silent to think.** This is the platform-specific trap and it is the one that costs people the interview. *(Candidate-reported.)* Zara reportedly reads a pause as *"answer finished"* and moves on — so a silent think burns the question. **Always narrate:** *"Let me think about that for a moment."* Then think out loud. If the report is wrong, you have lost nothing by narrating.
2. **Rambling into the time limit.** The fix is beat 1: answer first. If you run out of time, you want to have run out *after* the answer.
3. **Answering a question they didn't ask.** "Data quality" questions often invite you to talk about your favourite project. Don't. Answer the data-quality question, then use the project as evidence.
4. **Asserting a rubric instead of applying one.** If a question gives you criteria, use *their* criteria, in *their* words. Do not substitute your own framework and call it equivalent.
5. **Hiding the ambiguity.** If a question is genuinely underspecified, **say so and state the assumption you're making.** That is the correct answer to an ambiguity question, not a failure.
6. **Claiming a number you don't have.** Especially time saved or error-rate reduction. §6.4 covers the replacement move.

**And one recovery habit:** if you miss or misunderstand a question, **ask Zara to rephrase immediately.** Candidates report it as permitted and as the main recovery mechanism, and that you cannot scroll back through the transcript to re-read a question — micro1 does not publish either as a guarantee, but the advice is sound regardless.

---

## §2 — Topic 1: Data quality review & QA validation

### 2.1 The framework — memorise these six, in this order

This is the standard vocabulary of the field and it is what an evaluator expects to hear. Learn it as a checklist you can recite in 20 seconds.

| Dimension | The question it answers | How you check it |
|---|---|---|
| **Completeness** | Is anything missing? | Null counts, required-field coverage, row-count deltas against the source |
| **Accuracy** | Does it match reality / the source of truth? | Reconciliation against an authoritative source; spot-check with traceable records |
| **Consistency** | Do the same facts agree across tables and systems? | Cross-table joins, duplicate keys with conflicting values, format drift |
| **Timeliness** | Is it current enough to be used? | Freshness timestamps, lag between event and load, staleness thresholds |
| **Validity** | Does it conform to the rules it should? | Type, range, domain, regex and referential-integrity checks |
| **Uniqueness** | Is anything duplicated? | Primary/unique key enforcement, fuzzy-match review for near-duplicates |

**Say this out loud in the interview:** *"I run the six as a standard checklist — completeness, accuracy, consistency, timeliness, validity, uniqueness. Then I triage by cost: the cheap structural checks (completeness, validity, uniqueness) usually localise the problem before I spend on full reconciliation against the source — and reconciliation is the expensive one."*

**Why the order is stated that way, and not as a cost ranking.** The six are a standard checklist in a conventional order, not a cheap-to-expensive sequence. **Accuracy — full reconciliation against a source of truth — is the most expensive check on the list, and it is second.** If you claim the list is cost-ordered, the obvious follow-up is *"reconciliation is your most expensive step; why is it second?"* and the answer collapses. Say "standard checklist, then triage by cost" and the question never lands.

### 2.2 Validation vs review — the distinction that scores points

- **Review** is *finding* problems: profiling, anomaly detection, eyeballing distributions.
- **Validation** is *proving* a dataset meets defined rules, with a pass/fail outcome.

The strongest answer names the difference and then says why it matters: **"A review produces an opinion. A validation produces a gate. Only one of them can stop a bad number reaching a client."**

This is directly your ground truth — **and the mapping is the reverse of the obvious one.**

- **Optum is the gate.** Zero-tolerance pass/fail on high-volume federal enrollment transactions, with audit-ready documentation. That is **validation** in the strict sense: it proves a dataset meets defined rules, with an outcome.
- **The Black Piano agent is detection and recovery.** It finds a rule violation (a required field is missing), repairs it, and escalates only when it can't. That is **not** validation — it doesn't gate anything; it fixes.

So: **prevention is the audit habit, recovery is the agent.** Say which is which. If you file your gate experience under "review" and your repair agent under "validation", an interviewer who is listening will hear you misclassify your own work — and this is precisely the topic where that costs you.

### 2.3 The concrete example to have ready

**Black Piano — the self-healing data-quality agent.** You have a full walkthrough in [`icici_lombard_interview_prep.md` §4](icici_lombard_interview_prep.md). The 45-second version for this interview:

> "At Black Piano one recurring data-quality failure wasn't the numbers — it was **missing brand domains**, which broke logo rendering on client dashboards. That's a completeness failure with a client-visible symptom. I built an agent that resolves it: a deterministic reference-table lookup first, an LLM fallback for the long tail, then a **write-back to both the dataset and the lookup table** so the fix persists. Three retries on failure, then an email escalation for a human. The design point is the write-back — it turns a recurring model call into a one-time cost plus a free table lookup, so the system gets cheaper as it learns. The limitation is that I never instrumented the hit rate, so I can't tell you the split between table-resolved and model-resolved. That's the first thing I'd fix."

**Note what that answer does:** it names the quality dimension (completeness), the mechanism, the design rationale, and a real limitation — in under a minute. That is the template from §1.1, executed.

### 2.4 QA validation drills — rehearse these

**Q: "You're handed a dataset you've never seen. Walk me through your first hour."**
> "Profile before I trust anything. Row count and column count. Null rate per column, and which nulls are legitimate versus broken. Distinct values on the low-cardinality columns so I can see the domain. Min, max and distribution on the numerics, because a negative age or a date in 1970 tells me more than any summary statistic. Then I check the primary key for uniqueness and the foreign keys for referential integrity — orphaned rows are the failure that silently drops data from a join. Only then do I reconcile totals against the source system. And I write the checks down as rules, not as observations, so the next run is a validation rather than a repeat review."

**Q: "Two reports show different numbers for the same metric. How do you resolve it?"**
> "I assume the difference is real and find it, rather than assuming one is wrong. First I check whether the metric definitions actually match — the same name frequently means different filters, different date logic, or gross versus net. Then I trace both to source and check the join: an inner join silently drops unmatched rows, and that is the most common cause I've seen. Then time zone and cutoff boundaries. Then duplicates inflating one side. I resolve it by picking one definition, documenting it, and making both reports read from the same governed query — because reconciling the numbers without fixing the definition means it recurs next month."

**Q: "What's your approach to a pipeline that fails silently?"**
> "Silent failure is the worst class, because a pipeline that crashes gets fixed and a pipeline that loads bad data gets trusted. So I validate at the boundary: row-count expectations, null-rate thresholds, and a freshness check that fails if the data is older than expected. Any of those tripping should fail the load loudly rather than publish. I learned this the hard way — I've had a scoring configuration where a weight interacted with a formula and made an entire category return zero results. Nothing errored. The run completed and the summary looked fine. **Absences don't throw.** That's why the check has to be an explicit expectation about what should be there, not just a check that nothing crashed."

That last one is real, from JobAgents (the AI Safety track weight bug). It is one of your strongest stories because it is a genuine failure that taught a generalisable lesson.

---

## §3 — Topic 2: Judgment under ambiguity & documentation of rationale

This is the topic most candidates fail, because the instinct is to *pretend* the situation isn't ambiguous and answer confidently. The topic name tells you the expected behaviour: **name the ambiguity, choose a defensible path, document why.**

### 3.1 The four-step method

1. **Separate the ambiguity.** Is it in the *goal* (what outcome is wanted), the *scope* (which data/rows/timeframe), the *definition* (what the metric means), or the *constraint* (deadline, tooling, permissions)? Naming which one it is makes it tractable.
2. **State the assumption you are proceeding on** — explicitly, out loud.
3. **Choose the reversible option** where one exists. If two readings are both plausible, do the one that is cheap to undo, and say why.
4. **Document the rationale where the next person will find it** — not in your head, not in a chat message. In the query, the pipeline config, the ticket, or the table description.

### 3.2 What "documentation of rationale" means concretely

It does **not** mean "I left a comment." It means a record that lets someone else reconstruct *why*, months later, without you. In practice that is four things:

| Element | Example |
|---|---|
| **The decision** | "Excluded internal test accounts from the revenue metric." |
| **The reason** | "They inflate totals and are not customer transactions." |
| **The alternative rejected** | "Considered leaving them in and filtering at the dashboard, rejected because every downstream consumer would have to remember." |
| **The trigger to revisit** | "Revisit if internal accounts ever transact for real." |

**Say this in the interview:** *"A number without its rationale is an assertion. Six months later nobody can tell whether a filter was deliberate or a bug — and at that point the only safe move is to redo the analysis. Documenting the why is what makes the work reusable instead of disposable."*

This is the same instinct that produced the anti-fabrication guard in your own pipeline, and it is worth connecting out loud: **"the component that decides whether to believe the output"** is the through-line of everything you build.

### 3.3 Ambiguity drills

**Q: "You're asked for 'a report on sales performance'. What do you do?"**
> "I don't build it yet. That request has at least four ambiguities: the timeframe, the grain — by region, product, or customer — the definition of 'sales' (booked, shipped, or collected are three different numbers), and the audience, because an exec summary and an analyst appendix are different artifacts. I'd ask the two questions that change the work most — who's reading it and what decision it's meant to inform — and I'd state my assumption for the rest: 'I'm taking sales as booked revenue, monthly, last 12 months, by region and product; tell me if any of those is wrong.' That way I'm not blocked, and I'm not silently guessing either."

**Q: "You're told to deliver something you believe is wrong. What do you do?"**
> "I separate the deliverable from the concern. I'd say what I think the problem is, concretely and once — with the evidence, not the objection — and then ask whether there's context I'm missing. Often there is: a regulatory requirement, a stakeholder commitment, a definition I didn't know about. If there isn't, I'd still deliver, because it's their call, but I'd document the concern alongside the work so the record shows it was raised. What I won't do is quietly deliver something I think is wrong and say nothing, and I won't refuse to deliver a legitimate request because I disagree with a definition."

**Q: "You have incomplete data and a deadline. Go."**
> "First I find out whether the incompleteness is random or systematic, because that decides everything. Random gaps I can handle — state the coverage, report on what's there, flag the confidence. Systematic gaps — a whole region, a whole channel, the last three days — I can't paper over, because the answer will be wrong in a direction, not just noisy. So: quantify the gap, say plainly what the data can and cannot support, deliver the part that's sound, and put the rest in the open as a known limitation. **I'd rather deliver a smaller correct answer than a complete wrong one.** And I'd write down what the gap was, because a number produced under a known gap tends to get quoted later without the caveat."

---

## §4 — Topic 3: Rubric-based evaluation & guideline adherence

This is the most distinctive topic in the list, and it is the one that most signals what the work actually is: **judging outputs against written criteria, consistently, and showing your reasoning.**

### 4.1 The four rules of rubric adherence

1. **Use their criteria, not yours.** If a rubric says three things, you evaluate three things. Adding a fourth dimension — however sensible — is a guideline violation, and it is exactly what is being tested.
2. **Evaluate literally.** Score what the rubric says, not what you infer it means. If the rubric says "cites a source", a plausible unsourced statement fails — even if it's probably true.
3. **Score each criterion independently.** Do not let a strong overall impression lift a criterion that genuinely fails. Halo effect is the standard failure mode in rubric evaluation.
4. **Show the evidence per criterion.** The score should be defensible from the artifact alone. "Meets — because the output names the source in line 4" is a good rationale. "Meets — looks right" is not.

### 4.2 The structure to use when asked to evaluate anything

> **Criterion → Verdict → Evidence → Confidence**

Worked example — evaluating an AI-generated summary against a rubric:

| Criterion | Verdict | Evidence | Confidence |
|---|---|---|---|
| Factually grounded in the source | **Fails** | States a 12% decline; the source shows 8% | High |
| Covers all required sections | **Passes** | All four headings present | High |
| No unsupported claims | **Fails** | The decline figure is the same unsupported claim | High |
| Tone appropriate for the audience | **Passes** | Neutral, no jargon | Medium — audience not specified in the brief |

**Then the line that matters:** *"Two criteria fail on the same defect, and I've scored them separately rather than collapsing them, because the rubric asks about grounding and about unsupported claims as distinct requirements."*

That sentence demonstrates literal rubric adherence in the act of answering. It is worth rehearsing.

### 4.3 The harder case — when the rubric is wrong or silent

**Q: "The rubric doesn't cover the case in front of you. What do you do?"**

> "I score what the rubric does cover, and I flag the gap explicitly rather than inventing a criterion. If it's a genuine gap I'd note it as 'not covered by the rubric' with what I'd have scored and why, so the rubric owner can decide — that's useful feedback and it's not my call to make unilaterally. What I wouldn't do is stretch a criterion to fit, because that makes my scores inconsistent with everyone else's and quietly corrupts the dataset the rubric exists to produce."

**Q: "Two evaluators disagree on the same item. How is that resolved?"**

> "Disagreement is information about the rubric, not just about the item. First I'd check whether we applied the same criterion the same way — usually the rubric is ambiguous at exactly the point where two reasonable people diverge. If it is, the fix is to tighten the rubric wording and re-score the affected items, not to average the two scores. Averaging hides the ambiguity and keeps producing it. Where the rubric is clear and one of us misapplied it, the correct score stands and the misapplication is the thing to correct."

### 4.4 Why this connects to your real work — say it

You have unusually strong evidence for this topic, and it is worth naming directly:

- **JobAgents' anti-fabrication guard**: a resume that fails validation is never written to disk. It catches **8/8 seeded fabrications**. That is rubric adherence enforced by code — a written rule with a pass/fail gate.
- **The review invariants**: rather than asking a model to grade a model, the checks split by what each side is good at — set membership, regex and arithmetic go to code; only genuine judgment calls go to the model, and even then as an advisory that never erases a violation.
- **The line to quote:** *"A reviewer that returns pass for everything is worse than no reviewer, because it manufactures confidence in a verdict nobody verified."*

That last sentence is essentially a thesis statement for rubric-based evaluation, and you arrived at it by building the thing.

**The strongest single example you own for this topic is the BugAgents report-promotion gate.** It is a rubric with four hard criteria — scope match, HEAD match, non-empty reproduction, evidence files must exist — and a documented outcome: **2 reports promoted, 34 unverified candidates refused.** Use it like this:

> "I built a gate with four criteria that a report has to satisfy before it's treated as a finding. Two promoted; thirty-four were refused. The refusals are the number I'd defend hardest — a filter that promotes everything it's given has a refusal count of zero and no verification at all. It would look more productive on every dashboard and it would be worthless. **A filter's job is to refuse.**"

That is rubric adherence, severity discipline, and the false-positive/false-negative trade-off in one answer — and it maps onto micro1's own praise language almost word for word.

### 4.5 The four concepts micro1's feedback explicitly names — have an answer for each

micro1's post-interview feedback email names these as the difference between a strong and a weak evaluation. Each is a likely question, so have a position ready:

**1. "How do you keep your scoring consistent across a long batch?" (inter-rater reliability / calibration)**
> "Two ways. For myself, I re-check a fixed set of known items periodically to make sure my scoring hasn't drifted — the failure is gradual, so it needs a fixed reference point rather than a feeling. Across raters, you need a calibration set: a handful of items everyone scores independently, and then you compare. If two people diverge, that's information about the rubric wording, not about the item. You fix the wording, not the score."

**2. "How do you decide severity?" (severity taxonomy)**
> "I want a named, ordered scale with a stated test for each level, so the decision isn't taste. The test I default to is **impact and reversibility**: does it change the meaning of the output, does it reach a user, and can it be undone. A formatting defect and a wrong number are not the same class of problem even if both are 'errors', and collapsing them is how severity becomes noise. And I always say why it's *this* level and not the one above or below — that's what makes the call reviewable."

**3. "How do you score something that's partially correct?" (partial correctness)**
> "Only if the rubric allows it. If it's binary, it's binary, and inventing a middle band makes my scores incomparable with everyone else's. Where partial credit is allowed, I score per criterion rather than per output — so 'covers the required sections' can pass while 'no unsupported claims' fails, and the total reflects both. The thing I won't do is give a vague middle score because the output felt mostly fine. **'Mostly fine' isn't a criterion.**"

**4. "What makes feedback actionable?" (what's wrong, why, what next)**
> "Three parts, and the third is the one people skip: what's wrong, why it's wrong against the criterion, and what to do next. Feedback that only says 'this is incorrect' is a verdict, not feedback — the person receiving it can't act on it. And I cite the specific evidence: the line, the cell, the trace step. 'The reasoning was weak' is not reviewable; 'step 4 asserts a total the source doesn't support' is."

**One caution from the research, and it is a real trap:** some candidates report being assessed at a *higher scope* than the role warranted — asked to design rubrics for a role that applies them. If a question feels above the level of the job, **name the level you're answering at:** *"As the evaluator applying this rubric, I would X. Defining the rubric is the rubric owner's call, and I'd escalate that rather than decide it."* That answer is correct even if the question was mis-tiered.

---

## §5 — Topic 4: Spreadsheet proficiency (baseline)

"Baseline" means they are checking you are not bluffing. Precision beats breadth — name the function and what it is for, don't recite a list.

### 5.1 The functions to have at instant recall

| Need | Function(s) | The one-line explanation to give |
|---|---|---|
| Exact lookup | `XLOOKUP` (or `INDEX`+`MATCH`) | Preferred over `VLOOKUP` because it doesn't break when columns move and it can search leftward. `XLOOKUP` is Excel 2021+/365 and in Sheets. |
| Approximate / banded lookup | `XLOOKUP` with `match_mode` (**-1** = exact or next smaller, **1** = exact or next larger), or `VLOOKUP` with `TRUE` | For tiered rates and banding. **Get this right — it is a classic trap:** `XLOOKUP`'s approximate match does **not** need sorted data (it scans). **`VLOOKUP` with `TRUE` does** (first column must be ascending). Sorting is only required for `XLOOKUP` **binary search**, which is a different argument — `search_mode` 2 / -2. |
| Conditional aggregation | `SUMIFS`, `COUNTIFS`, `AVERAGEIFS` | The workhorse. Multiple criteria, and it doesn't need the data sorted. |
| Conditional logic | `IFS`, `IF`, `AND`, `OR` | `IFS` over nested `IF` for readability. |
| Error handling | `IFERROR`, `IFNA` | `IFNA` is better when you only want to trap "not found" and still see real errors. |
| Text cleaning | `TRIM`, `CLEAN`, `SUBSTITUTE` (Sheets: same, plus `SPLIT` and `REGEXEXTRACT`) | Trailing spaces and non-printing characters are the most common cause of a lookup that "should" work. **The trap: `TRIM` removes ASCII space only and `CLEAN` strips chars 0–31 — a non-breaking space, `CHAR(160)`, survives both.** That is the classic web-pasted value, and the fix is `SUBSTITUTE(x,CHAR(160)," ")`. Also note `TEXTSPLIT`/`TEXTBEFORE`/`TEXTAFTER` are **Excel 365 only — not Excel 2019/2021, and not Google Sheets.** |
| Deduplication | `UNIQUE`, `COUNTIF` | `COUNTIF` on the key identifies duplicates; `UNIQUE` gives the distinct set. On 50,000 rows, bound the range (or use a pivot) — a full-column `COUNTIF` per row is quadratic and will crawl. |
| Ranking / top-N | `LARGE`, `SMALL`, `RANK` | |
| Dates | `EOMONTH`, `EDATE`, `DATEDIF`, `YEARFRAC` | Month-end and elapsed-time calculations. |
| Pivot tables | — | Group, aggregate, drill down. Say you use them for exploration, not as the final artifact. |
| Data validation | — | Dropdowns and rules that stop bad input at entry — the cheapest data-quality control there is. |
| Conditional formatting | — | For flagging outliers and blanks visually. |
| Repeatable cleaning steps | Power Query (Excel) · query sheet or Apps Script (Sheets) | For cleaning you can **refresh** rather than redo by hand. **Power Query is Excel / Power BI only — it is not in Google Sheets.** |

### 5.2 The answers that demonstrate judgment, not memorisation

**Q: "How would you find duplicates in a list of 50,000 rows?"**
> "Depends what counts as a duplicate. Exact duplicates: `COUNTIF` on the key column, filter anything above 1, and inspect before deleting — because duplicates are sometimes legitimate, like two orders with the same customer and amount on the same day. On 50,000 rows I'd bound the `COUNTIF` range or use a pivot, rather than run a full-column `COUNTIF` per row — that's quadratic and it crawls, and the answer is the same either way. Near-duplicates — same entity, slightly different spelling — are a different problem and a formula won't solve them; that's fuzzy matching, and I'd want to know the tolerance before I started merging, because a false merge destroys two real records and is much worse than a missed duplicate."

**Q: "A `VLOOKUP` returns `#N/A` and you can see the value is there. What's wrong?"**
> "Ninety percent of the time it's a type or whitespace mismatch — the lookup value is text and the table is numeric, or one side has a trailing space. I'd check with `LEN` and `TRIM`, and check the type with `ISNUMBER`. Then the range: `FALSE` for exact match, because the default approximate match silently returns a wrong-but-plausible answer, which is far worse than an error. Then whether the lookup column is actually inside the table array, and whether the sheet reference is absolute."

**Q: "How would you make a spreadsheet report that doesn't break next month?"**
> "Separate the layers: raw data untouched in one sheet, cleaning steps in another, calculations in a third, presentation in the last. No manual edits to raw data ever, because that's unreproducible. Use a repeatable cleaning mechanism so refreshing is a single action rather than a repeat of last month's manual work — in Sheets that's a query sheet or an Apps Script job, in Excel it's Power Query. And put the definitions and filters somewhere visible, so the next person can see *why* a row was excluded rather than guessing."

**If asked about Excel versus Google Sheets — read this twice.** Your verified stack includes **Google Apps Script** and **auto-exported Google Sheets pipelines**. That is real, hands-on spreadsheet automation and it is worth naming.

But be precise about what it is and is not. Your ground-truth profile lists **no spreadsheet tool as a named skill** — Sheets appears inside project descriptions, Apps Script is listed, and **Excel and VBA are not there at all.** So:

- **Do not invent Excel, VBA, or Power Query depth.** "Baseline" is the bar and you clear it on the fundamentals above, but a fabricated answer under time pressure falls apart on the first follow-up — and this is an interview whose scoring language explicitly rewards *specificity*. You cannot fake specific.
- **The honest, strong framing:** *"I work in Google Sheets rather than Excel — I've built automated export pipelines and used Apps Script to drive them, and I use formulas and pivot tables for analysis. If you ask me for a specific Excel-only feature I'll tell you I haven't used it and describe the equivalent operation I'd do in Sheets or SQL."*
- **The pivot that turns it into a strength:** *"The spreadsheet work I do is mostly the repeatable kind — cleaning and shaping data that feeds a pipeline. I'd rather automate a cleaning step than perform it manually each month, because a manual step isn't reproducible and a formula is."*

That answer is honest, specific, and demonstrates exactly the reproducibility instinct the rubric rewards.

**One rule for the whole spreadsheet section: name the platform with the function.** If the interviewer is working in Excel and you work in Sheets, say which of these you have actually used rather than which you have read about. Several functions in the table above are Excel-only and several Sheets idioms have no Excel equivalent — and being caught reciting a function you have never opened is worse than saying "I haven't used that one."

---

## §6 — Topic 5: Error & Edge-Case Detection

### 6.1 The categories to run through — every time

A checklist beats intuition when you're timed. Run these in order:

1. **Boundaries** — zero, one, maximum, negative, empty. The values at the edge of the valid range, not the middle.
2. **Nulls and blanks** — including the difference between `NULL`, empty string, `0`, and `"N/A"`. They behave differently in joins and aggregates in ways that matter: **`NULL` never matches `NULL` in an equi-join while `''` matches `''`**, and **both are ignored by `COUNT`** — so a "missing values" count depends entirely on which of the two you actually have. `0` and `"N/A"` are neither, and both will silently pass a null check.
3. **Duplicates** — exact and near.
4. **Type and format** — numbers stored as text, dates as strings, locale-dependent decimal and date formats.
5. **Time** — time zones, month and quarter boundaries, leap years, the 31st of a short month, daylight-saving transitions, and the "last 7 days" question of whether today is included.
6. **Joins** — inner joins silently dropping unmatched rows; many-to-many joins multiplying rows and inflating totals. **This is the single most common cause of a wrong-but-plausible number.**
7. **Aggregation** — double counting, and averages of averages.
8. **Ordering and pagination** — top-N queries that aren't deterministic because of ties.
9. **Permissions and scope** — rows the query can't see, which look like missing data.
10. **Currency, units and scale** — thousands versus units, INR versus USD, and percentages stored as 0–1 versus 0–100.

### 6.2 The habit that makes you good at this

**Ask what the output would look like if the bug were present.** If a wrong answer and a right answer look identical, you have no detector — that's the whole problem with silent failure. Your own line, from the data-quality agent: *a missing domain is visibly broken, but a **wrong** domain renders the wrong logo and looks fine.* A confident wrong answer is more dangerous than an obvious gap. Say that.

### 6.3 Edge-case drills

**Q: "Here's a query that reports monthly revenue. What could be wrong with it?"**
> "I'd check six things. The join — if it's an inner join to a customer or product table, any transaction without a match silently disappears, and the total is low with no error. Whether it's a many-to-many join inflating the total. The date filter boundaries — whether the month end is inclusive, and whether timestamps are in UTC while the business thinks in local time, which moves transactions across month boundaries. Refunds and cancellations — whether they're netted or excluded, which changes the number by more than most people expect. Currency — whether multi-currency revenue is summed without conversion, which is meaningless. And duplicates from a re-run or a re-loaded batch. Then I'd sanity-check the total against the source system, because reconciliation catches all six at once."

**Q: "A test passes but the feature is broken. How?"**
> "The test asserts the happy path and the bug is at a boundary, or the test asserts that something ran rather than that it produced the right result. A test that only ever passes is worthless — the useful question is whether the check *fires when the rule is violated.* I've built checks that way deliberately: my review invariants were validated by deliberately violating every rule and asserting each one fires, which is the only way to know a checker isn't just returning pass."

**Q: "What's an edge case people miss in date logic?"**
> "Time zones, and it's not close. A timestamp stored in UTC and reported in IST moves transactions across day and month boundaries, so a monthly report can be wrong by a day's worth of revenue and still look completely normal. The second is inclusive versus exclusive end dates — 'between 1 Jan and 31 Jan' means different things depending on whether the underlying column is a date or a timestamp, and with a timestamp you silently lose everything after midnight on the 31st."

### 6.4 When you don't have the number

The interview will likely ask something quantitative about your own work — *"how much time did that save?"*, *"what was your error rate?"* If you don't have a measured figure, **do not invent one.** Use this shape:

> "I don't have a measured figure for that — I built the mechanism before the instrumentation, which is backwards. What I can tell you is the mechanism: the reference table now answers the routine cases deterministically, so the recurring cost trends toward zero model calls. If I did it again, measuring the hit rate from day one would be the first thing I'd add."

**Why this wins:** it is honest, it shows you know what you'd measure, and it demonstrates exactly the "documentation of rationale" instinct the interview is testing. A fabricated percentage is the single fastest way to fail an evaluation-focused interview — the person reading your answer is a professional evaluator.

---

## §7 — Practice set: 12 questions, timed

Answer each in 90 seconds, out loud, with the §1.1 template. Record yourself once.

| # | Question | Topic |
|---|---|---|
| 1 | Walk me through how you'd validate a dataset you've never seen. | DQ/QA |
| 2 | Tell me about a data quality problem you found and fixed. | DQ/QA |
| 3 | What's the difference between a review and a validation? | DQ/QA |
| 4 | You're asked for a report with almost no specification. What do you do? | Ambiguity |
| 5 | Tell me about a time you had to make a call without complete information. | Ambiguity |
| 6 | How do you document why a decision was made? | Rationale |
| 7 | Here's a rubric. Evaluate this output against it. | Rubric |
| 8 | The rubric doesn't cover this case. Now what? | Rubric |
| 9 | Two evaluators disagree. How do you resolve it? | Rubric |
| 10 | How do you find duplicates in 50,000 rows? | Spreadsheet |
| 11 | What could be wrong with a query that reports monthly revenue? | Edge cases |
| 12 | A test passes but the feature is broken. How is that possible? | Edge cases |

**Score yourself on four things, 1–5 each:** Did I answer first? Did I state the criteria? Did I give a concrete example? Did I name a limitation or edge case? Anything below 4 on the last two is where the interview is won or lost.

---

## §8 — Pocket card

**The one-sentence positioning for this interview:**

> *"I've spent my career on whether data can be trusted — nine years auditing federal enrollment transactions at Optum, then three and a half years building the pipelines and the quality gates on the client side. The interesting engineering was never getting a system to produce output; it was building the component that decides whether to believe the output."*

**Framework to recite:** completeness → accuracy → consistency → timeliness → validity → uniqueness.

**Rubric answer shape:** criterion → verdict → evidence → confidence.

**Ambiguity answer shape:** name the ambiguity → state your assumption → choose the reversible path → document the why.

**Edge-case checklist:** boundaries · nulls · duplicates · types · time · joins · aggregation · ordering · permissions · units.

**Say:**
- 18 automated ETL pipelines → BigQuery → Looker Studio across 18 industry sectors *(Black Piano)*
- Self-healing data-quality agent — table-first, LLM fallback, write-back, 3 retries, email escalation *(Black Piano)*
- 10+ client dashboards, 30+ analytical reports, Python `Pi-API` package *(Pi Software)*
- 9 years CMS enrollment audit at Optum — data quality as a gate, not a report
- JobAgents' guard catches **8/8** seeded fabrications; review invariants **0 failures**, and every check fires when violated

**Never say:**
- A number that isn't in [../config/profile.md](../config/profile.md) — especially a time-saving percentage or an error rate for your own work
- Any job title above **Data Analyst**; no people-management experience exists
- Independent projects as employer or client work
- The BugAgents vendor, asset, or vulnerability class
- That BugAgents findings were "disclosed", "accepted", "paid", **or "resolved"** — nothing has been submitted
- Any **production users, revenue, adoption, or customer** claim for any of your projects — none exist
- That you **authored** the AgentSwarm manuscripts — the agent authors are `A001_DarkMatter` / `A002_QuantumCosmos`
- "Peer-reviewed" or "published in a journal" about either AgentSwarm manuscript
- "We" about solo work
- **Excel, VBA, or Power Query depth** — not in your verified skills. See §5.

**Full forbidden list:** [`outreach_templates.md` §6](outreach_templates.md) — it binds here too.

**Before you click start:** run the free mock at `interview.micro1.ai/mock-interview` two or three times · read the pre-interview screen for the skills list and whether a written task portion is included · seed your intro to end on the data-quality agent · never go silent — narrate your thinking · if you miss a question, ask for a rephrase.

---

*Companion files: [micro1_ai_agent_evaluator_prep.md](micro1_ai_agent_evaluator_prep.md) (the 20-minute interview), [micro1_platform_research.md](micro1_platform_research.md) (platform intel, verified vs anecdotal), [icici_lombard_interview_prep.md](icici_lombard_interview_prep.md) (recruiter context + project deep dives), [interview_guide.md](interview_guide.md) (full project deep-dives), [../config/profile.md](../config/profile.md) (binding ground truth).*
