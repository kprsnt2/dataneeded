# ICICI Lombard — Interview Debrief & Technical Round Prep

**Interview 1:** done, 2026-10-15. **Next:** technical round, format/date to be confirmed.
**Interviewer confirmed:** it is the **Agentic AI** role, and there **will be a technical round**. Formal dress, join 10 minutes early.

---

## §0 — The 60-second read

1. **Your multi-model answer was good — genuinely.** The response-variance → schema-normalisation → drift argument is the correct architecture, and you explained it in plain language. Two things would have made it stronger: saying the word **contract**, and noting that **routing** must be deterministic.
2. **Your self-hosting suggestion was half right, and the wrong half could hurt you.** The **privacy** argument is strong — arguably the most important point anyone made in that interview. The **cost** argument is usually backwards. §3 tells you how to correct it before the technical round, because they may well ask you to defend it.
3. **They told you "you're the first to implement".** That means greenfield. The technical round will be architecture and judgement, not trivia. §4.
4. **You cited rAsh Score and the live numbers have moved past your README.** Live site says **300 tracked brands, 20 industry cohorts**; your README says 279 and 19. **Cite the live figures.** §5.
5. **rAsh Score is a much better project for this role than you realise.** It is a live multi-model evaluation harness with four scored dimensions and a debate arena — which is *exactly* the problem this job is about. §5.
6. **Fix your ground truth before the next round.** rAsh Score is not in `config/profile.md`, so every agent in your pipeline — and this prep — has been treating it as if it doesn't exist. §5.4.

---

## §1 — Scorecard on the first interview

| What they asked | What you did | Verdict |
|---|---|---|
| **Your work automation, and how you used AI in it** | Explained the automation, the pipeline, and the human fallback | **Good.** This was your strongest material (§4C of the main prep) and you used it. |
| **Multi-model: how you'd solve the problem** | Response-format variance across models → structured output via system prompt → JSON segmentation → drift on model updates → models work well with structured I/O | **Strong.** This is a real architectural answer, not a keyword answer. |
| **Explained a project** | rAsh Score healthcare leaderboard | **Good instinct** — but see §5: you undersold it, and cited stale numbers. |
| **Closing suggestion on self-hosting** | Privacy for health data + lower LLM cost | **Half right.** Privacy: strong. Cost: usually wrong. §3. |

**The one thing you did that most candidates don't:** you offered a strategic suggestion unprompted, and you framed it as *"irrespective of my selection"*. That reads as someone who cares about the problem rather than the job. It is a genuine differentiator — **provided the advice holds up**, which is why §3 matters.

---

## §2 — Your multi-model answer, refined

What you said was correct. Here is the sharper version, so you can deliver it again in the technical round with more precision.

### 2.1 The three points you made, named properly

**1. Response-format variance is a real engineering problem, not a quirk.**
> *"Ask three models the same question and you get three shapes — a numbered list, a paragraph, a table. If your pipeline parses prose, it breaks the moment a model changes its house style. That's not a bug you fix once; it's a permanent fragility."*

**2. The fix is a schema, enforced at the boundary.**
> *"So you don't parse prose. You constrain the output to a schema — JSON is my preference, XML works, some teams use function calling — and you validate against it before anything downstream touches it. The important part is what that buys you: **the model's output becomes a contract you can test**, instead of text you have to interpret."*

**Say the word "contract."** It is the difference between describing a technique and describing an engineering principle, and it is the same idea as your BugAgents gate: a check that can reject.

**3. Model updates are a source of drift, and you detect it rather than assume it.**
> *"Models get updated underneath you. A prompt that returned clean JSON for six months can start returning JSON wrapped in a sentence. So you monitor: a fixed set of golden inputs, run against the live model on a schedule, checking that the output still validates and the values are still stable. When the schema validation rate drops, you know before your users do."*

**Why this connects to rAsh Score:** you have literally built this. rAsh Score queries multiple models with standardised prompts and scores them — that *is* a multi-model harness with drift observation. Say so (§5).

### 2.2 The two things you should add next time

**1. Routing must be deterministic — not a model deciding.**

If they push on "how do you handle multiple models", the strong answer is:

> *"I'd keep the routing decision itself out of the models. Which model handles which task should be an explicit rule — by task type, by cost ceiling, by data-sensitivity tier — not a model choosing. If a model decides which model to call, you've added a non-deterministic step to your control plane, and now you can't explain why a given claim went to a given model. In a regulated decision that's indefensible."*

That is a real, senior position, and it maps directly onto claims.

**2. Fallback needs to be defined, not improvised.**
> *"Multi-model also means multi-failure-mode. If the primary returns an invalid schema three times, what happens? In my own work the answer is bounded retries and then a defined escalation — never an unbounded loop, and never a silent default."*

This is your data-quality agent's design (3 retries → email escalation) applied to model routing. Same instinct, and you have already shipped it.

### 2.3 The one-liner to have ready

> *"Structured output isn't about making the model tidy. It's about converting an unreliable narrator into a testable component. Once the output validates against a schema, everything downstream can be deterministic — and in a claims decision, deterministic is the only thing you can audit."*

---

## §3 — Your self-hosting suggestion: what to keep, what to fix

You asked what I think. **Honest answer: you were right about the risk and wrong about the economics — and the economics is the part they're most likely to probe.**

### 3.1 The privacy argument — keep this, it's your best point

This is genuinely strong, and for an Indian health insurer it is close to the centre of the problem:

- Health data is the most sensitive category you can process, and under the **DPDP Act 2023** — which is mid-rollout on a staggered timetable — there is **no separate "sensitive data" tier**: every claim document carries equal statutory weight. (Sourced in [`health_claims_domain_research.md`](health_claims_domain_research.md).)
- If a third-party model API sees claim documents, you have created a data-flow you must be able to describe, justify, and audit.
- **A model you host means the data never leaves your perimeter** — and the compliance conversation gets dramatically simpler.

That instinct — *"this data is too sensitive to hand to someone else's endpoint by default"* — is exactly right, and it is the kind of thing a claims or compliance stakeholder remembers.

### 3.2 The cost argument — usually backwards, and here's why

**Self-hosting is rarely cheaper than API calls.** The reasons:

| Cost you take on | What it looks like |
|---|---|
| **GPU capacity** | Either capex on hardware or a per-hour cloud GPU bill — and it accrues whether or not claims arrive. API billing scales with usage; your GPU bill does not. |
| **ML engineering** | Someone has to serve, quantise, version, monitor and update the model. That is a headcount, not a line item. |
| **Model capability** | The models you can self-host at reasonable cost are smaller than frontier APIs. On medical-necessity reasoning, a smaller model is a real quality regression — in the highest-stakes part of the pipeline. |
| **Utilisation** | Self-hosting only wins at **high, steady** utilisation. Bursty claims volumes mean idle GPUs. |

**The rule of thumb:** API calls win at low-to-moderate volume and for hard reasoning. Self-hosting wins at **very high, steady volume on narrow, simple tasks** — classification, extraction, routing — where a small fine-tuned model can match a frontier model at a fraction of the marginal cost.

### 3.3 The answer that would have been stronger — and still makes your point

Do not abandon the suggestion. **Sharpen it.** The correct enterprise answer is usually not "self-host everything" but **tier the data and match the deployment to the tier**:

> *"I'd start by classifying what actually flows through the pipeline. Policy numbers and member identifiers can go to a frontier model under a zero-retention, no-training enterprise agreement — that's a contractual control, and it's what most insurers do. But clinical documents — discharge summaries, investigation reports, diagnosis detail — I'd want to keep inside our perimeter.*
>
> *And that's where self-hosting becomes interesting, but only for the right tasks. Not for medical-necessity reasoning, where you want the strongest model you can get. For the high-volume, narrow work — document classification, field extraction, routing — where a smaller model you host can do the job at a fraction of the marginal cost and the data never leaves.*
>
> *So my suggestion isn't 'replace the API'. It's: tier the data, keep clinical content in-perimeter, self-host the high-volume narrow tasks, and use frontier APIs — under a no-training agreement — only where you genuinely need the reasoning."*

**Why this is better than what you said:** it keeps your privacy insight, drops the cost claim that doesn't survive scrutiny, and shows you understand that this is a **data-classification decision** rather than a build-versus-buy preference. That is a more senior answer, and it is harder to argue with.

### 3.4 If they challenge you on it in the technical round

**"Self-hosting is expensive — did you consider that?"**
> *"Yes, and I'd have put it better. Self-hosting wins at high, steady volume on narrow tasks; it loses on bursty volume and on reasoning quality. My actual point was about data residency for clinical documents, and the right version of that argument is tiering the data rather than replacing the API everywhere."*

**Correcting yourself cleanly is a strength, not a weakness.** A candidate who says *"I'd have put that better, here's the sharper version"* reads as someone who thinks rather than someone who performs. Do not defend the cost claim.

### 3.5 One thing your suggestion proved

**You have actually done the thing you recommended.** BrandXY is a **fine-tuned self-hosted model** (GPT-OSS-20B, LoRA/QLoRA, 76.5% vs 25.5% baseline). If self-hosting comes up, you are not theorising:

> *"I've done this at small scale — I fine-tuned and released my own model rather than only calling APIs, so I know both the cost shape and the maintenance burden. It's not free, and it's not always the right call."*

That converts a suggestion into experience.

---

## §4 — Preparing for the technical round

They told you **"you're the first to implement"** — so expect greenfield design questions, not trivia. Prepare these five.

### 4.1 The architecture answer (from §3.3 of the main prep)

Have the eight-step pipeline ready to sketch: intake and classification → extraction (IDP/OCR) → **deterministic policy and coverage rules engine** → medical necessity → fraud scoring → routing (auto-approve / human review / **no auto-decline**) → explanation generated **from the decision trace** → immutable audit log.

**Land the two non-negotiables:** the rules engine must not be an LLM, and denials must not be straight-through.

### 4.2 The governance answer

The IRDAI Master Circular on Health Insurance Business (**ref IRDAI/HLT/CIR/PRO/84/5/2024, dated 29.05.2024**) already constrains the design:

- **Cashless pre-auth decided within one hour**; final discharge authorisation within **three hours**, with delay costs borne by the insurer from shareholders' funds.
- **"No claim shall be repudiated without the approval of PMC or a three-member sub-group… called the Claims Review Committee."**

**Say this:** *"The routing policy I'd propose isn't a design preference — the regulator has effectively already written it. Auto-approve within limits, human approval for every repudiation."* That is a very strong thing to say in a technical round, because it shows you read the rules before proposing the architecture.

### 4.3 The evaluation answer

They will ask how you know the system works. You have the best answer in the room:

> *"Never a model grading a model — that rubber-stamps. My own review invariants were validated by deliberately violating every rule and asserting each check fires. A checker that only ever returns pass is worse than no checker, because it manufactures confidence. For claims I'd want a labelled historical set, per-decision-type accuracy, and a monitored schema-validation rate as the early-warning signal for model drift."*

### 4.4 The multi-model answer

§2. Add the routing point and the drift-detection point.

### 4.5 The honest-limits answer

They will probe what you don't know. Have §4.3 of the main prep ready, and lead with the sharpest one: **you have not run a claims desk.** Say it before they find it.

---

## §5 — rAsh Score — verify your numbers, and use this project properly

### 5.1 Your numbers are stale

I checked the live site on 2026-10-15:

| | Your README | **Live site** |
|---|---|---|
| Tracked brands | 279 | **300** |
| Industry cohorts | 19 | **20** |
| Scoring dimensions | 4 | **4** ✓ |

**Cite the live figures: 300 brands, 20 industry cohorts.** The README is behind — same stale-document problem your canonical profile warns about. The live site is the authority.

**Also confirmed live:** the four models named on the site are **ChatGPT, Gemini, Claude and Groq**.

**On Groq vs Grok — get this right before you name it.** I checked your source: the codebase references **both**, and they are different things:

- **Groq** — the fast-inference API provider (`api.groq.com`, `GROQ_API_KEY`). **82 references in your source**, and your own code comments call it the *"fastest inference"* path and use it as a **fallback** for insights and reports. This is the one that is genuinely wired up.
- **Grok** — xAI's model (25 references, plus 33 for `xai`). It appears in a Vertex AI comment and some config, but it is **not one of the four named on your live site**.

**So name four: ChatGPT, Gemini, Claude, Groq.** If asked which you use most, your own code answers it — **Groq for speed as the fallback path**, and your `.env.example` lists OpenAI, Gemini, Vertex, NVIDIA and Groq as configured providers.

**If they ask about provider mix, this is a better answer than a model list:** *"I run four providers and I route by task — OpenAI for the scheduled pipeline, Gemini as the direct fallback, and Groq where I want fast inference. Having four wired means a provider outage degrades the run rather than stopping it."* That is a multi-provider resilience story, which is more relevant to an insurer than which model is cleverest.

### 5.2 Why this project is better for this role than you seem to think

Read your own README description back: it **queries multiple foundation models with standardised evaluation prompts** and computes a composite score across **four independently-scored dimensions** — recommendation, sentiment, prominence, accuracy.

**That is a multi-model evaluation harness with a scoring rubric.** It is the same class of system as the "AI Agent Evaluator" work and the same class of problem as judging whether a claims model is behaving.

And you have more in there: a **multi-agent debate arena** (Agent Pro-A, Agent Pro-B, The Judge), **text-to-SQL** analyst chat, an **LLM-optimisation strategy generator**, and daily **GitHub Actions** pipelines into **Turso/LibSQL** with a Next.js dashboard on Vercel.

**The pitch for the technical round:**

> *"I've built a live multi-model evaluation platform — it queries ChatGPT, Gemini, Claude and Groq with standardised prompts, scores each brand across four independent dimensions, and runs daily so I can see perception shift over time. Three hundred brands, twenty industry cohorts. The reason it's relevant here is that it forced me to solve the exact problem you asked me about: getting comparable, structured output out of models that all answer differently, and detecting when a model update changes the answer."*

**That is a much stronger answer than the healthcare leaderboard alone**, because it demonstrates the multi-model engineering *and* the evaluation discipline in one project.

### 5.3 Be ready for the obvious follow-up

**"What did you learn about model differences?"** Have a specific, honest observation ready — e.g. which model formats most consistently, which is most verbose, which drifts most on updates. **Only say what you have actually observed in your own data.** You have 300 brands across four models; you have real observations. Do not generalise into claims about model quality you cannot support from your own runs.

### 5.4 Fix your ground truth — this matters beyond this interview

**rAsh Score is not in `config/profile.md`.** That means every agent in your own pipeline — and this prep — has been treating the project as non-existent, and your tailored resumes cannot cite it.

Add it, with the **live** figures and the live URL, as a featured project. It belongs there: it is live, it is verifiable, it demonstrates multi-model evaluation, and it is arguably the most directly relevant thing you have built to an "Agentic AI" role at an insurer.

**Suggested entry:** name, one-line purpose, live URL, stack (Next.js, Turso/LibSQL, GitHub Actions, Vercel, multi-provider model APIs), the four scoring dimensions, and the verified counts — with the live site as the source, the same way your other metrics are recorded.

---

## §6 — Questions for the technical round

1. **"What does the pipeline look like today — is anything automated, or is this greenfield?"** — "First to implement" suggests greenfield; confirm it.
2. **"Which decisions do you want automated first — approvals, or the document handling upstream?"** — tests whether they have thought about sequencing.
3. **"Where would the model sit, and where would the rules sit?"** — if they say "the model decides coverage", you have found your first piece of work.
4. **"What's the data-residency position — would clinical documents go to a third-party API, or stay in our environment?"** — your §3 insight, asked as a question rather than a lecture. Much stronger.
5. **"How do the medical reviewers feel about this? Are they shaping it or receiving it?"** — the best predictor of whether the project succeeds.
6. **"Who signs off on an automated decision, and what's the audit expectation?"** — governance ownership.
7. **"What does the first milestone look like, and by when?"** — scoped means real.
8. **"Is the team building this, or is there a vendor?"** — determines whether you'd be writing specs or integrating someone's product.
9. **"What's the stack — Python, cloud, any existing claims platform we'd integrate with?"** — practical, and it tells you how much greenfield there really is.
10. **"What's the band and grade for this role, and what does the total package include?"** — still unresolved. Ask it.

---

## §7 — Pocket card for the technical round

**Opening, if they ask you to introduce yourself:**
> M. Pharmacy → 9 years Optum (Claims Associate → CMS enrollment audit) → 3.5 years data and agentic AI. Then: *"the interesting engineering was never getting a model to produce output — it was building the component that decides whether to believe the output."*

**If they ask about multi-model:**
> *"Structured output isn't about making the model tidy — it converts an unreliable narrator into a testable component. Schema-constrained output, validated at the boundary, with routing kept deterministic and drift detected by monitoring the validation rate."*

**If they ask about architecture:**
> Eight-step pipeline. **Rules engine for anything contractual; model only where judgement is needed. Auto-approve behind guardrails; never auto-decline — the IRDAI Master Circular already requires Claims Review Committee approval for repudiation.**

**If they ask about evaluation:**
> *"Never a model grading a model. Validate the checker by deliberately violating every rule and asserting it fires."*

**If self-hosting comes up:**
> *"Tier the data. Clinical documents stay in-perimeter; high-volume narrow tasks are candidates for a self-hosted small model; frontier APIs under a no-training agreement only where you need the reasoning. I've fine-tuned and released my own model, so I know both the cost shape and the maintenance burden — it isn't free."*

**The project to lead with:**
> rAsh Score — **300 brands, 20 industry cohorts, 4 dimensions, 4 models, daily pipelines.** Multi-model evaluation harness. Live.

**Never say:**
- **"PMP certified / qualified / trained"** — prepared, exam not taken
- Any title above Data Analyst for held employment
- That BugAgents findings were disclosed, accepted, paid, **or resolved**
- Any production users, revenue or adoption claim for your independent projects
- That you authored the AgentSwarm manuscripts
- Any ICICI Lombard claim-settlement or financial figure — you have none sourced
- **The README's 279/19 figures** — cite the live 300/20

---

*Companion files: [`icici_health_claims_interview_prep.md`](icici_health_claims_interview_prep.md) · [`health_claims_domain_research.md`](health_claims_domain_research.md) · [`../config/profile.md`](../config/profile.md)*
