# micro1 — "AI Agent Evaluator" AI Interview Prep (~20 minutes)

> **Source of truth for the format:** the invitation screenshot, preserved at [assets/micro1_ai_agent_evaluator_20min.png](assets/micro1_ai_agent_evaluator_20min.png).
> **Source of truth for every fact about you:** [../config/profile.md](../config/profile.md).
> **Platform context:** [micro1_platform_research.md](micro1_platform_research.md) — verified facts separated from candidate anecdote.

---

## §0 — What this interview is, and the trap in it

The invitation says, verbatim:

> *"Please note that this interview will take ~20 minutes with each question having a limited time for a response. You will answer by speaking, or typing. Ensure you're in a quiet spot with a stable internet connection. This interview will be recorded and available in your profile link."*

> *"You will be interviewed on these topics:"*
> - Following Detailed Instructions Exactly
> - Hands-On Use of AI Tools
> - Judging When to Step In
> - Custom questions defined for the job

**Twenty minutes is short.** Roughly 8–12 questions at 90–120 seconds each. There is no room for a long preamble — every answer must land its point in the first sentence.

### Platform facts that change how you prepare

Grades below are per [micro1_platform_research.md](micro1_platform_research.md), which separates micro1's own published statements from candidate testimony. **Do not treat a candidate-reported item as platform policy.**

1. **VERIFIED — the interviewer is a voice AI called Zara, auto-scored, with a real-time verdict.** micro1's own guide promises *"a real-time result indicating whether you meet micro1's global certification criteria."* There is no human to read the room. Prepare for a machine-readable answer structure.
2. **CANDIDATE-REPORTED — never go silent.** Candidates independently report that a pause is read as *"answer finished."* Narrate your thinking: *"Let me think about that for a moment."* This is the highest-value behavioural change for a 20-minute window, where a lost question is a lost 10% of the interview — and it costs nothing if the report turns out to be wrong.
3. **VERIFIED — rehearse on the real product first, and it is free.** `interview.micro1.ai/mock-interview`, plus `micro1.ai/interview-prep`. Do it two or three times. It is the same application as the live interview.
4. **VERIFIED — read the pre-interview screen before you click start.** micro1 staff confirm it states *"skills assessed, duration, etc."*, and that whether a **written or task portion** is included is **role-specific**. Free information that resolves the biggest format unknown.
5. **CANDIDATE-REPORTED — seed your intro deliberately.** Zara reportedly generates follow-ups from the *end* of your introduction. End on the thing you want drilled — the evaluation and verification work, not the physics papers. Even if the mechanism is different, ending your intro on your strongest material is free insurance.
6. **CANDIDATE-REPORTED — ask for a rephrase if you miss a question.** Reported as permitted and the main recovery mechanism; not published by micro1 as a guarantee. The same reports say there is a live transcript but **no scroll-back**. Either way: if you miss it, ask rather than guess.
7. **VERIFIED — this is a certification gate, not a job interview.** micro1 states: *"Certification does not guarantee immediate placement."* Passing puts you in a vetted pool for a client hiring manager to review — and the documented ceiling on that review is 30 days. **Treat a pass as eligibility, and keep your other applications running in parallel.**

### The trap — read this twice

Your instinct will be to prove you are a **builder**. You build multi-agent swarms, autonomous pipelines, evaluation harnesses. The temptation is to turn every answer into an architecture discussion.

**This interview is not testing whether you can build an agent. It is testing whether you can be trusted to judge one.**

Read the three topics again. "Following Detailed Instructions **Exactly**." "**Judging** When to Step In." This is an **evaluation and operations** role. It is closer to quality assurance than to engineering. The evaluation is asking: *can this person apply someone else's rubric to an AI system's output, notice when something is wrong, and know the boundary of their own authority?*

**Your builder background is the supporting evidence, not the headline.** Use it to prove you understand *why* rules exist — then demonstrate that you follow them anyway. The single most valuable thing you can signal is:

> *"I've built the systems that decide whether to believe an AI's output. So I know exactly how they fail, and I know that the person evaluating them has to be more disciplined than the system."*

That is your positioning for all 20 minutes.

---

## §1 — How to answer in a 20-minute window

### 1.1 The template — tighter than the 43-minute one

| Beat | Time | Rule |
|---|---|---|
| **1. Direct answer** | 5s | First sentence answers the question. No wind-up. |
| **2. The concrete instance** | 30–45s | One real example. Not three. |
| **3. The boundary** | 15–20s | The limit, the escalation trigger, or the honest gap. |

**No beat 4.** Twenty minutes doesn't have room. If you have more to say, the interviewer will ask a follow-up — and a follow-up question is a better outcome than a monologue.

### 1.2 The three failure modes in this format

1. **Over-answering.** Talking for three minutes because you know a lot. In a 20-minute interview that costs you two other questions.
2. **Answering the question you wish they'd asked.** Especially: turning "how do you use AI tools?" into "here's my agent architecture." Answer the actual question.
3. **Performing autonomy.** Saying you'd handle something yourself when the correct answer is escalate. "Judging When to Step In" is testing whether you know your own limits. Claiming no limits fails the topic.

---

## §2 — Topic 1: Following Detailed Instructions Exactly

**This topic is literal, and it is the easiest to fail by being helpful.** The test is not "can you follow instructions" — it is "will you follow them *exactly*, including when you think you know better."

### 2.1 The six things that break instruction-following

Before you answer anything in this section, run this list:

1. **Output format.** If it says "reply with JSON only", any prose around the JSON is a failure. If it says "three bullets", four is a failure.
2. **Scope.** "Summarise section 2" is not "summarise the document." Extra content is not a bonus — it's a deviation.
3. **Order.** If steps are numbered, the sequence is part of the instruction, not a suggestion.
4. **Terminology.** If the guideline says "label it `Unsupported`", then `Unsupported claim` is a different label.
5. **Explicit exclusions.** "Do not use external sources" is binding even when a source would help.
6. **Implicit length and tone.** "One sentence" means one sentence. This is where over-delivery does the most damage.

### 2.2 The method to state out loud

> "I read the instruction twice and pull out the **constraints** as a list before I start — format, scope, order, terminology, exclusions, length. Then I do exactly that, and if I think a constraint is wrong I still follow it and flag the concern separately. That separation matters: the deliverable stays compliant, and the feedback still reaches the person who can change the guideline."

**Say the second half explicitly.** It is the answer to the obvious follow-up ("what if the instruction is bad?"), and it demonstrates that compliance and judgement are not in conflict.

### 2.3 Why you actually believe this — the evidence

You have an unusually strong, specific reason to hold this position, and it comes from your own work:

- **JobAgents' guard rejects non-compliant output rather than warning about it.** The rule that generated text may not attribute independent projects to an employer is enforced in code — and the model violated the prompt-level version of that rule *anyway*, in capitals, while producing fluent output. Your conclusion: **"If the rule isn't enforced by something that can reject the output, it isn't a rule — it's a suggestion."**
- **The review invariants split by capability** — set membership, regex and arithmetic to code; only genuine judgment calls to a model, and even then as an advisory that never erases a violation. That is guideline adherence designed rather than hoped for.
- **The BugAgents abort.** Any out-of-scope host or offensive tool aborts the agent at the turn boundary. Not warned, not logged-and-continued. **Aborted.**

**The one-sentence version:** *"I've watched a model violate an explicit instruction while producing output that read perfectly. That's why I follow guidelines literally — I've seen what happens when something doesn't."*

That answer is credible in a way that "I'm detail-oriented" never will be.

### 2.4 Instruction-following drills

**Q: "The guideline says reply in exactly two sentences. You need three to answer well. What do you do?"**
> "Two sentences. If the third point is essential I'd compress it into the second sentence, and if it genuinely can't be compressed I'd deliver two sentences and note separately that the guideline may need a length exception for this class of item. Changing the format unilaterally makes my output incomparable with every other evaluator's, and comparability is the entire point of a fixed format."

**Q: "You're given a rubric and a guideline that conflict. Which wins?"**
> "I don't resolve it myself — that's a judgement call above my authority, and picking one silently means my scores are inconsistent with everyone else's. I'd apply the more specific instruction if one is clearly more specific, document which I applied and why, and raise the conflict immediately so it can be resolved for everyone. A conflict that gets resolved once for one evaluator is a conflict that recurs for all of them."

**Q: "How do you make sure you haven't missed a constraint?"**
> "I extract them into a list before I start rather than holding them in my head — format, scope, order, terms, exclusions, length. Then I check the output against the list before submitting. The failure mode isn't not knowing the rule, it's having read it and then not checking. So the check is a step, not an intention."

---

## §3 — Topic 2: Hands-On Use of AI Tools

**"Hands-on" means they will probe for real usage, not vocabulary.** The failure mode is a keyword wall. The winning mode is: name the tool, say what you did with it, say where it broke.

### 3.1 Lead with what you genuinely use

Everything below is in your verified stack. Lead with the first two groups; the rest is depth if asked.

| Tool / capability | Your real, verified usage |
|---|---|
| **Claude 4.x, Gemini 2.5/3.x, GPT-OSS 120B/20B, DeepSeek 4.1** | Multi-model routing, fallback chains, and A/B evaluation across providers. You run agents on multiple substrates and compare them. |
| **Agent CLIs / harnesses** (omp, pi, agy, Antigravity, DeepSeek Harness) | Orchestrating long-horizon agents, and — importantly — *discovering and working around undocumented CLI quirks* by probing. |
| **MCP / FastMCP** | Built a custom MCP tool letting non-technical marketing and sales teams generate publication-ready, data-grounded content from a one-line prompt. |
| **Prompt and system design** | System prompts, tool schemas, guardrails, bounded autonomy, escalation design. |
| **Evaluation harnesses** | Independent verifier design, oracle checks, numerical audit, hash-chained audit ledgers. |
| **LoRA/QLoRA fine-tuning** | BrandXY — GPT-OSS-20B on AMD MI300X, **76.5% vs 25.5% baseline**. |
| **Human-in-the-loop design** | Email escalation in the data-quality agent; the promotion gate in BugAgents. |

### 3.2 The answer shape that beats a tool list

**Q: "How do you use AI tools in your work?"**

> "Three ways, and I'd rank them by how much judgement each needs.
>
> **As a builder** — I design and run multi-agent systems. JobAgents scores jobs deterministically with zero model calls and only sends the shortlist to a model; that's the pattern I default to, cheap deterministic filter first, model on the residue.
>
> **As a user** — I built an MCP tool that lets non-technical marketing and sales generate publication-ready, data-grounded content from a one-line prompt. The engineering there wasn't generation, it was **grounding** — the model reads real numbers from auto-exported Sheets pipelines instead of inventing plausible ones.
>
> **As a sceptic** — which is the part that matters for this role. I've built the layer that decides whether to believe the output: an anti-fabrication guard that validates generated text against a ground-truth file *before* it's written to disk, and catches 8/8 seeded fabrications. I've also watched a model violate an explicit prompt rule while producing fluent output. **Fluency is not correctness, and the artifact looks identical either way. Only the evidence distinguishes them.**"

That answer covers all three topics in one breath: real usage, real tools, and the evaluation instinct the role needs.

### 3.3 The honest-gap answer — prepare this, you will need it

You have **not** shipped production work in ChatGPT Enterprise, Copilot, Cursor, or enterprise AI platforms. If asked directly, do not claim it. Use:

> "I've used ChatGPT for content and analysis work — at Black Piano I built a weekly AI insights pipeline with it, auto-published to a client-facing site. My deeper hands-on work is with Claude, Gemini and open models through agent harnesses, where I'm doing orchestration and evaluation rather than chat. I haven't shipped with Copilot or Cursor in a team setting. I'd expect the tooling to transfer quickly because the underlying skills — prompt structure, grounding, checking output — don't change with the wrapper."

### 3.4 Questions they may ask about AI usage

| Question | Your spine |
|---|---|
| "When do you *not* use an AI tool?" | When the answer must be deterministic and auditable, when the cost per item is too high at volume, or when the failure is silent and expensive. JobAgents' scoring is arithmetic with zero model calls for exactly this reason. |
| "How do you check AI output?" | Against ground truth, not against plausibility. The guard validates against a source-of-truth file in code before anything is persisted. And I check that the *checker* works by deliberately violating every rule and asserting it fires — a checker that only returns pass is worthless. |
| "How do you prompt for reliability?" | Give the model a falsifiable task rather than a confirming one, constrain the output format, and don't ask a model to grade a model without a rubric. Also: state what "done" looks like, because most prompt failures are underspecification, not model weakness. |
| "What's a limitation of LLMs you've hit?" | Confident, well-formed wrongness — and the fact that it's indistinguishable from correct output by inspection. Also context limits: my AI Eco swarm bounds living memory under 4,000 words deliberately, because unbounded state makes behaviour a function of history rather than purpose. |
| "Have you fine-tuned?" | Yes — LoRA/QLoRA. BrandXY: GPT-OSS-20B on AMD MI300X, 76.5% vs 25.5% baseline, to measure and steer recommendation bias. Single run, no external replication — say that part too. |
| "What tools do you use daily?" | Name what's true: the agent CLIs, Claude/Gemini/open models, Python, BigQuery, Looker Studio, Git, Google Apps Script. Don't pad. |

---

## §4 — Topic 3: Judging When to Step In

**This is the highest-signal topic in the interview.** It is asking about *calibrated authority*: knowing the difference between a decision you should make and one you should escalate. In AI-training and evaluation work this is the core competency — an evaluator who escalates nothing is unreliable, and one who escalates everything is useless.

### 4.1 The decision framework — memorise the two axes

**Axis 1 — Reversibility.** Can this be undone cheaply? If yes, act. If no, act **only** where the guideline is explicit — and log it. Where it isn't explicit *and* it isn't undoable, escalate.

**Axis 2 — Coverage and confidence.** Coverage: is this case clearly inside the guidelines? Confidence: would you defend this call to a reviewer? **These are independent** — a case can be clearly covered and still be one you shouldn't be the one deciding. Coverage decides *who owns the rule*; confidence decides *whether you should be the one applying it*.

| | **Guideline covers it clearly** | **Genuine edge case / not covered** |
|---|---|---|
| **Reversible** | **Decide.** Apply the rule, document it. | **Decide the item, escalate the gap.** Score it as "not covered", state what you'd have scored and why, and raise the gap to the guideline owner. The *item* is yours to call; the *rule* is not. Do not stretch a criterion to fit. |
| **Irreversible / high-impact** | **Decide, but log it.** The rule is clear, but the consequence isn't undoable — so the record matters as much as the call. | **Escalate.** Not covered *and* not undoable is exactly what escalation exists for. |

**In every cell:** escalate if your confidence is below the threshold you'd defend (§4.2 item 6). The matrix tells you who owns the decision; it is not a licence to act on a call you couldn't justify to a reviewer.

**Then the sentence that makes it land:**

> "The asymmetry is deliberate. Acting on a reversible case costs a correction. Acting on an irreversible one costs something that can't be corrected. So the bar for acting alone goes up as reversibility goes down — and the escalation path has to be cheap enough that using it isn't a punishment."

**The distinction to say out loud if pushed:** *"I separate the item from the rule. I'll decide the item — that's my job — but a gap in the guideline isn't mine to fill unilaterally, because my fix would only apply to me and would make my scores inconsistent with everyone else's. So the item gets scored and documented, and the gap gets escalated."*

### 4.2 The categories where you always step in

Name these if asked for a list:

1. **Anything outside your scope or authority** — no matter how obvious the answer looks.
2. **Irreversible actions** — deletions, submissions, anything customer-facing, anything that leaves your workspace.
3. **Safety, legal, privacy, or regulatory exposure** — including PII you weren't cleared to see.
4. **Genuine guideline gaps** — the case the rubric doesn't cover.
5. **Conflicts of interest** — including the ones that flatter you.
6. **Confidence below the threshold you'd defend** — if you wouldn't defend the call to a reviewer, escalate it rather than ship it.
7. **Anything that requires an identity, an account, or an acceptance of terms that isn't yours.**

### 4.3 The evidence you have for this — it is genuinely strong

This topic is where your builder background converts directly into credibility. Every example is real and verified:

- **BugAgents aborts rather than warns.** Any out-of-scope host or offensive tool aborts the agent at the turn boundary. And it isn't theoretical — **a live run was aborted exactly this way** when a hunter reached for a host that wasn't on the tooling allowlist. *"A safety control that has only ever been exercised by its own unit test is an untested control."*
- **BugAgents refuses to submit.** Findings are submission-ready drafts; **nothing has been submitted**. Submission requires accepting a program's terms and disclosing identity, so it stays a human action by design. The gate promoted **2** reports and refused **34**.
- **The data-quality agent escalates by email** for the cases it can't resolve, after three bounded retries. Autonomous on the routine, explicitly non-autonomous on the residue.
- **Hard budget and kill switch** — `MAX_SPEND_USD`, `MAX_TURNS_PER_AGENT`, `MAX_WALL_CLOCK_MINUTES`, and a `STOP` file that halts the hunters at the next turn boundary. A no-finding verdict is a valid, recorded outcome.
- **The AI Eco swarm's debt-pruning gate is set at zero false positives** — deliberately asymmetric, because deleting a live file is unrecoverable in a way that leaving dead code is not.

**The line to deliver:** *"I've built four systems where the escalation boundary was the design decision, not an afterthought. The rule I keep arriving at is the same one: **act where it's reversible and inside the guidelines, escalate where it isn't, and make the escalation path cheap enough that using it isn't a failure.**"*

### 4.4 Judgement drills

**Q: "An agent's output is 90% right and you're on a deadline. Ship or escalate?"**
> "Neither, yet — first I find out what the 10% is. If it's formatting or tone, I fix it and move on. If it's a factual error, a wrong number, or an unsupported claim, the deadline is irrelevant, because a wrong number that ships gets quoted later without the caveat. The 90% figure is the trap: a plausible output is exactly what a wrong output looks like. So the question isn't how much is right, it's *what kind of thing is wrong*."

**Q: "You spot an error in a colleague's evaluation. What do you do?"**
> "Go to the colleague first, with the specific item and the specific criterion, rather than going over them. Most disagreements are rubric ambiguity, and if the rubric is ambiguous that's a finding worth raising for everyone. If we still disagree after applying the rubric literally, then it goes to whoever owns the rubric — because the resolution should change the guideline, not just this one score. What I wouldn't do is silently change their score or let it stand without saying anything."

**Q: "How do you decide you've done enough checking?"**
> "When I've checked against the criteria rather than against a feeling, and when a further check wouldn't change the verdict. Practically: every criterion has a verdict and a piece of evidence. If I can point at the evidence for each one, I'm done. If I'm re-reading the same thing hoping to feel better about it, that's not verification, that's anxiety — and it's a sign the rubric is underspecified."

**Q: "When should a human be in the loop, in one sentence?"**
> "When the action can't be undone, when the guideline doesn't cover the case, or when the consequence of being wrong lands on someone other than me. Everything else, I should be able to decide and document."

---

## §5 — The custom job questions

The invitation lists *"Custom questions defined for the job"* — role-specific questions set by whoever is hiring. You cannot know them in advance, but the categories for an AI Agent Evaluator role are predictable. Prepare the *shape*, not the answer.

### 5.0 What the work actually is — so your custom answers land in the right register

micro1 publishes the product this role feeds. Its agent-evaluation platform describes four steps, and **your interview topics map onto them one-to-one**:

| micro1's stated process | Your interview topic |
|---|---|
| **Evaluation design** — *"Define success criteria, rubrics, and scoring for the agent's task"* | Rubric work (also the 43-minute interview) |
| **Failure diagnosis** — *"review agent outputs and identify where, why, when, and how the agent fails"* | Judging When to Step In · Error & Edge-Case Detection |
| **Expert training data** — targeted data addressing the failure modes | Following Detailed Instructions Exactly |
| **Monitor reliability** — re-evaluate as models, prompts and rules change | Hands-On Use of AI Tools |

micro1's own engineering language adds the vocabulary it uses internally: *"isolate that exact trace, **grade the reasoning chain**, and correct the failure mode"*; *"graded multi-turn traces, your **failure taxonomies**"*; *"Continuous Calibration."* And its data-generation pipeline explicitly turns expert judgment into *"new environments, rubrics, variations, and **edge cases**."*

**Use these phrases, and mean them:**

- **"grade the reasoning chain, not just the final answer"** — the core of trace evaluation.
- **"failure taxonomy"** — a named, ordered classification of how the agent fails, so failures are countable rather than anecdotal.
- **"where, why, when, and how it failed"** — the four-part diagnosis.
- **"continuous calibration"** — re-checking your own scoring against a fixed reference as models and rules change.
- **"edge-case test set"** — a deliberate set of boundary cases used to check whether a rule actually fires.
- **"human review beyond automated evals and LLM-as-judge"** — micro1's own stated differentiator, and a position you independently arrived at by building review invariants rather than LLM-grading-LLM.

**The one-line version of why you're credible here:** *"I've built the layer that decides whether to believe an agent's output — and I've watched it catch things a fluent answer would have hidden."*

### 5.1 The five categories to expect

| Category | Typical question | Your answer's spine |
|---|---|---|
| **Agent trace evaluation** | "Here's a transcript of an agent's steps. Where did it go wrong?" | Find the first divergence, not the final error. Look for: an unsupported assumption early, a tool called with wrong arguments, a result ignored, a loop, or a success claim with no evidence. |
| **Rubric writing** | "Write criteria to evaluate this output." | Make each criterion **independently checkable** and **binary or clearly banded**. Avoid criteria that need taste to apply — those produce disagreement. |
| **Error taxonomy** | "Classify these failure types." | Separate *capability* failures (couldn't do it) from *compliance* failures (didn't follow the rule) from *honesty* failures (claimed it did). Honesty failures are the serious class. |
| **Ambiguity escalation** | "The guideline is silent on this item." | Score the item as "not covered" and state what you'd have scored and why — then escalate the **gap**, not the item, to the guideline owner. Do not stretch a criterion to fit, and do not invent a rule that only you will apply. |
| **Tool-usage judgement** | "When should the agent call a tool versus answer directly?" | Call when the answer depends on a fact outside the model's reliable knowledge or needs to be current, verifiable, or auditable. Answer directly when it's reasoning over what's already in context. |

### 5.2 The universal fallback when you don't know

If a custom question lands outside your experience, **say so and reason from first principles out loud.** That is a legitimate and often strong answer:

> "I haven't worked with that specific setup, so let me tell you how I'd approach it rather than pretend to know. First I'd find the guideline that covers it — if there isn't one, that's the finding. Then I'd identify what the output is supposed to be, and check whether it's there and whether it's true. Then I'd look for the failure classes I know generalise: unsupported claims, confident wrongness, a step that claims success without evidence, and scope drift. And I'd document the verdict with the evidence per criterion, because an undocumented verdict is just an opinion."

**Never bluff.** The person assessing you on an evaluation role is assessing exactly this.

### 5.3 The "partial correctness" question — expect it, it's named as a gap

micro1's post-rejection feedback email — **reproduced by one candidate**, and consistent with micro1's published question bank and its Cortex product language — flags *"how to score partial correctness"* as something candidates handle weakly. Have this ready:

> "Only if the rubric allows it. If it's binary, it's binary — inventing a middle band makes my scores incomparable with everyone else's. Where partial credit is allowed, I score **per criterion** rather than per output, so 'covers the required sections' can pass while 'no unsupported claims' fails, and the total reflects both. What I won't do is give a vague middle score because the output felt mostly fine. **'Mostly fine' isn't a criterion.**"

And the sibling question — **"how do you keep your scoring consistent across a long batch?"**

> "Two ways. For myself, I re-check a fixed set of known items periodically to confirm my scoring hasn't drifted; the failure is gradual, so it needs a fixed reference rather than a feeling. Across raters, you need a **calibration set** — a handful of items everyone scores independently, then compare. If two raters diverge, that's information about the rubric wording, not about the item. You fix the wording, not the score."

---

## §6 — Practice set: 10 questions, 20 minutes total

Answer each in 90 seconds or less, out loud, with the §1.1 template. Two minutes per question is the real pace — practise to it.

| # | Question | Topic |
|---|---|---|
| 1 | Tell me about yourself in 60 seconds. | All |
| 2 | How do you make sure you follow instructions exactly? | Instructions |
| 3 | What do you do when an instruction conflicts with your judgement? | Instructions |
| 4 | How do you use AI tools in your daily work? | Tools |
| 5 | How do you verify AI output? | Tools |
| 6 | When do you decide *not* to use AI? | Tools |
| 7 | When do you escalate instead of deciding? | Judgement |
| 8 | An agent's output is mostly right and you're on deadline. | Judgement |
| 9 | The guideline doesn't cover the case in front of you. | Judgement |
| 10 | How would you evaluate whether an AI agent performed well? | Custom |

**Score yourself 1–5 on:** Did the first sentence answer the question? Did I give one concrete example? Did I name a boundary or escalation trigger? Was it under 90 seconds?

---

## §7 — Before you sign anything (commercial realities)

**This section is not about the interview. It is about what comes after, and it is the part that costs people money.** All of the following is well-corroborated candidate testimony — commercial grievance, not fraud. micro1 is a real company: micro1, Inc., a San Francisco address, named executives, mainstream press coverage, and a large employee-staffed community. The "fake company" worry is unfounded. The *contract* worries are not.

**What is verified:**
- Pay is *"hourly **or** per task (depending on your project), at the rate fixed during onboarding"*, paid biweekly through Deel in USD. **Two contract shapes, and the difference matters enormously.**
- The advertised range for **AI Agent Task Evaluator** is **$20–$45/hr**. India is **not** on micro1's geographic exclusion list, so you are eligible.
- micro1's Candidate Privacy Policy states it may use *"de-identified information collected from interviews, including audio, video, transcripts, and assessment results, to train and enhance our proprietary machine learning models."* It also states it does **not** share that data with AI model companies for *their* training. The opt-out is **account deletion** (`talent.micro1.ai/delete-account`).
- Certification requires **government-issued ID**.
- The automated assessment *"will be reviewed by a human evaluator before a final decision is made"*, and there is an appeal route via `privacy@micro1.ai`.

**What candidates repeatedly report — treat as risk, not fact:**
- **Advertised rate ≠ contracted rate.** Multiple reports of the advertised hourly figure being multiplied down — 0.667×, 0.5×, 0.375×, even 0.125× — when the actual placement was as a Trainer or Reviewer rather than the advertised role.
- **Per-task completion is defined by the client.** *"As determined by Client's project leadership"* — with no objective completion test, and reports of long unpaid waits when a project pauses mid-review.
- **Onboarding and screening hours may be unpaid or capped** below the time actually taken.
- **Same role, materially different rates** across postings.
- **30-day limbo** is normal between certification and a client decision.

**The five things to get in writing before signing — ask for all five:**

1. **Rate basis:** is this hourly or per-task?
2. **The multiplier and the role you are contracted as** — Trainer, Reviewer, or the role advertised.
3. **The per-task definition of "complete"**, and who determines it.
4. **The review SLA** — how long between submission and payment.
5. **"What happens to my completed-but-unreviewed tasks if the project pauses?"**

**One candidate's rule is the right rule:** *"If there is no clear answer, do not accept the project."*

**On quoting your rate:** you state your expected rate during application, and the contract is *"at the rate fixed during onboarding"* — so the number you enter is consequential, and candidates report being unable to raise it afterwards. **Quote within the advertised band for the role.** Do not reflexively bottom out to look competitive; several candidates report that under-quoting did not help them get selected and left them stuck low.

**Two safety notes:**
- micro1's official sender domains are **`@micro1.ai`, `@micro1.io`, `@micro1.co`** — and nothing else. Anything from another domain claiming to be micro1 should be treated as untrusted.
- **`microonejobs.com` presents as micro1 but is not on micro1's own sitemap.** Treat it as untrusted.

---

## §8 — Pocket card

**Positioning, one breath:**

> *"I build autonomous agent systems — and the part I care about is the component that decides whether to believe the output. I've watched a model break an explicit instruction while producing fluent output that read perfectly. That's why I follow guidelines literally, check output against ground truth rather than plausibility, and escalate the cases the guidelines don't cover."*

**The three topic answers, compressed:**
- **Follow instructions exactly** → extract the constraints as a list before starting; follow them even when you disagree, and raise the concern separately.
- **Hands-on AI tools** → builder, user, and sceptic. Name real tools; name where they broke.
- **Judging when to step in** → reversible + inside the guidelines = decide. Irreversible or not covered = escalate. Make escalation cheap.

**The four sentences worth memorising:**

1. *"If the rule isn't enforced by something that can reject the output, it isn't a rule — it's a suggestion."*
2. *"Fluency is not correctness — the artifact looks identical either way. Only the evidence distinguishes them."*
3. *"A reviewer that returns pass for everything is worse than no reviewer, because it manufactures confidence in a verdict nobody verified."*
4. *"The escalation path has to be cheap enough that using it isn't a punishment."*

**Say:**
- Self-healing data-quality agent — table-first, LLM fallback, write-back, 3 retries, email escalation *(Black Piano)*
- 18 automated ETL pipelines → BigQuery → Looker Studio across 18 industry sectors *(Black Piano)*
- MCP tool for non-technical teams — grounded in auto-exported Sheets data, not invention *(Black Piano)*
- JobAgents: guard catches **8/8** seeded fabrications; **22,839** scores with **zero model calls**
- BugAgents: **34 refused, 2 promoted**; a live run aborted on a scope violation
- BrandXY: GPT-OSS-20B, **76.5% vs 25.5%** baseline — single run, no external replication

**Never say:**
- A number that isn't in [../config/profile.md](../config/profile.md)
- Any title above **Data Analyst**; no people-management experience exists
- Independent projects as employer or client work
- The BugAgents vendor, asset, repository, or vulnerability class — cite the project and severities only
- That BugAgents findings were "disclosed", "accepted", "paid", **or "resolved"** — nothing has been submitted
- Any **production users, revenue, adoption, or customer** claim for any of your projects — none exist
- That you **authored** the AgentSwarm manuscripts — the agent authors are `A001_DarkMatter` / `A002_QuantumCosmos`
- "Peer-reviewed" or "published in a journal" about either AgentSwarm manuscript
- "We" about solo work
- That you use tools you haven't used. The gap answer in §3.3 is stronger than a bluff.
- **Excel, VBA, or Power Query depth** — not in your verified skills. See the spreadsheet note in [`micro1_data_analyst_prep.md` §5](micro1_data_analyst_prep.md).

**Full forbidden list:** [`outreach_templates.md` §6](outreach_templates.md) — it binds here too.

**Before you click start:** run the free mock at `interview.micro1.ai/mock-interview` two or three times · read the pre-interview screen for the skills list and whether a written portion is included · seed your intro to end on the work you want drilled · never go silent — narrate your thinking.

---

*Companion files: [micro1_data_analyst_prep.md](micro1_data_analyst_prep.md) (the 43-minute interview), [micro1_platform_research.md](micro1_platform_research.md) (platform intel), [icici_lombard_interview_prep.md](icici_lombard_interview_prep.md), [interview_guide.md](interview_guide.md), [../config/profile.md](../config/profile.md).*
