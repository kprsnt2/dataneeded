# ICICI Lombard — "Agentic AI / Health Claims Automation" Interview Prep

**Interview:** tomorrow. **Format:** not yet known — confirm on the call.
**The three inputs you have, and they do not agree:**

| Source | What it says |
|---|---|
| **Recruiter, on the phone** | New project in Mumbai, **relocation required**, build agents that auto approve/decline/process **health claims** with GenAI. Said **₹22 LPA is the max**. |
| **The JD** | *"Product Owner: Health Claims Automation and Generative AI"*, Department: **Health and Analytics**, Location: **Mumbai**, **"Full-Time – Work From Office"**. Wants a **medical background + health insurance claims experience**. |
| **The interview invite** | Title: **"Agentic AI"**. |

> **Ground truth for everything about you:** [../config/profile.md](../config/profile.md). **Companion research:** [health_claims_domain_research.md](health_claims_domain_research.md) (claims vocabulary, lifecycle, regulation — sourced).

---

## §0 — The 60-second read

1. **The money is the one open item — and you're in a better position than you think.** He said **22 was max**, then in the same call said **"we can negotiate it."** Both cannot be true, so **22 is an opening, not a cap.** Your strongest argument is not "I want more" — it's that **13 LPA in your own house with no rent is not comparable to 22 LPA renting in Mumbai.** §2.
2. **The real product is a decisioning system, not a chatbot.** They want claims to move with less human touch. The single most valuable thing you can say in this interview: **auto-approval is tractable and auto-decline is not** — because a wrong approval costs money, and a wrong denial is a regulatory event. The IRDAI Master Circular has already written that routing policy into law (§3.2).
3. **Your fit is real but not where the JD points.** The JD asks for a claims operator. You are not one. But it *also* asks for someone who can make **"automated claims decisions explainable, auditable, and aligned with regulatory requirements"** — and that is precisely what you have spent three years building. §4.
4. **Two facts on your resume answer the JD's hardest filters — and both are buried.** You hold an **M. Pharmacy** (the JD's first requirement) and you started at Optum as a **Claims Associate**. Say both out loud in your first 30 seconds. §4A.1b.
5. **The 9 years at Optum is your strongest asset here — and your biggest inflation risk.** It is **US Medicare/Medicaid enrollment audit**, *not* claims adjudication. Bridge it honestly or it becomes the thing that loses you the room. §4.2.
6. **Lead with BugAgents.** The promotion gate — **four criteria, 2 promoted, 34 refused** — is structurally the same problem as claims adjudication, and the refusal count is the number that makes you credible. §4A.3.

---

## §1 — Resolve the money question (do this today, in writing)

Send one message. Short, warm, specific. It costs you nothing and it protects you.

```
Hi Swarnim, thanks again for the call — looking forward to tomorrow.

Two quick things so I come prepared:

1. The invite says "Agentic AI" and the JD is "Product Owner: Health Claims
   Automation and Generative AI". From our call I understood it's a blend of
   both — owning the claims automation roadmap and working hands-on with the
   tech teams. Is the interview assessing the product-ownership side, the
   agentic AI side, or both? Happy to be considered either way; I just want to
   bring the right examples.

2. On compensation — I mentioned 25–30 LPA and I understood 22 LPA was the
   ceiling for the band. I'd rather align on that before we invest time
   tomorrow, because relocation to Mumbai changes my cost base. If 22 is firm,
   I'd like to understand the full picture — relocation support, joining bonus,
   and the review cycle — so I can make a fair decision.

Happy to discuss either on the call first if that's easier.
```

**Why send this rather than just showing up:**

- **The scope question is not pedantry.** "Own the roadmap" and "build the agents" are assessed differently. Knowing the weighting tells you which examples to lead with.
- **The comp point must be on record before the interview.** He has told himself you are flexible. If you say nothing, you have effectively agreed.
- **It signals seniority.** Candidates who clarify scope and comp before an interview read as experienced, not difficult.

**If he pushes back on clarifying comp before the interview,** that is information: it usually means the band is genuinely hard-capped and they are hoping the interview creates sunk-cost pressure. Better to know now.

> **Resolved, no longer an open question:** the JD says *"Work From Office"* and the recruiter said relocation is required. Those agree. The earlier "mail said WFH" reading was a misread of **Work From Office** — there is no conflict to chase.

---

## §1A — It's a blended role. That is your opportunity *and* the risk

You have now heard from two sources that the role is **Product Owner + agentic AI for claims approval**, and the JD supports that: it asks for roadmap ownership *and* hands-on collaboration with developers, architects and data teams. The invite title confirms the AI half.

### Why this is good news for you specifically

**A pure Product Owner role would have been the harder interview.** They would have wanted years of backlog ownership, sprint metrics, and stakeholder ritual — and you have never held the title. A pure AI-engineer role would also have been harder, because they want the claims domain.

**A blend is exactly the gap you fill.** Almost nobody in that hiring pool has both halves:

- Claims-domain people (medical background, TPA or insurer ops) generally **cannot** assess whether an agent architecture is sound, or why a rules engine must not be an LLM.
- AI engineers generally **cannot** speak to adjudication, pre-auth, leakage or why a denial is a regulated event.

You sit in the middle: **pharmacy degree + nine years in regulated healthcare audit + three years building agentic systems with hard controls.** That is the blend they are describing, and you should say so explicitly:

> *"The way you've described it — owning the roadmap and working hands-on with the tech team — is actually the combination I'd want. I've spent nine years in regulated healthcare audit, so I understand why a decision has to be defensible, and three years building agentic systems, so I know what it takes to make one behave. Most people have one half of that."*

### The risk you must name — and turn into a question

**A blended role often means the mandate is not yet defined.** Sometimes it is genuine: a small team where one person must do both. Sometimes it means two stakeholders want different hires and nobody has decided. The failure mode is real — you spend three months negotiating what the job is instead of doing it.

Do not treat this as a red flag. Treat it as **the most useful thing you can probe**, because asking it well demonstrates exactly the product judgement they claim to be hiring for. Ask:

> *"When you say it's a blend — who owns the roadmap decision, and who owns the technical decision? And in the first six months, is the priority getting the automation live, or getting the requirements and controls right?"*

Then listen carefully. **A crisp answer means a real role. A vague answer means you would be defining the job yourself** — which is fine, but it should change what you negotiate for, and it means the first 90 days are a scoping exercise, not a delivery one.

### The ratio question — ask it plainly

The single most clarifying question available to you:

> **"What proportion of this role is product ownership versus hands-on work with the agents and the models?"**

- **70/30 toward PO** → they want a requirements-and-stakeholders person who is AI-literate. Lead with §7 (PO craft), the user stories, the prioritisation answer.
- **50/50** → the blend you described. Lead with §3.2 (the auto-approve/auto-decline asymmetry) *and* §7.2 (the user stories). Show you can move between the two registers in one conversation.
- **30/70 toward hands-on** → they want a builder who can talk to claims. Lead with the BugAgents gate, the escalation design, and the architecture in §3.3.

**You can answer all three.** The only thing that changes is which example you open with.

### The depth they are actually testing

Whatever the ratio, the JD's own sentence tells you the bar: *"Ensure that automated claims decisions are explainable, auditable, and aligned with internal policies and applicable regulatory requirements."*

**That single line is where the product and technical halves meet** — and it is where you are strongest. The Product Owner must specify that the explanation is a requirement, not a nice-to-have. The engineer must build it so the explanation comes from the decision trace rather than a model narrating a decision it never made. Being able to say both halves of that sentence, in one breath, is the whole interview:

> *"As the product owner I'd write it into the acceptance criteria: every automated decision must be reconstructable from its recorded rule path. As the person who'd work with your engineers, I'd insist the explanation is generated from that trace — never reconstructed afterwards by a model, because then you get a plausible narrative that isn't the actual reason, and in a regulated decision that is worse than no explanation."*

---

## §2 — The money conversation, honestly

### 2.1 What actually happened on that call — the full sequence

Now that you've given me the real numbers, the call reads very differently from how it first looked:

| # | What was said | What it means |
|---|---|---|
| 1 | He mentioned **a 30% hike** would be applied | A formula. On your **13 LPA** that is **~17 LPA** — so his own stated rule does not reach 22. Remember that. |
| 2 | You explained **13 LPA** is a Data Analyst package, and that you'd since built AI skills and applied them in your current role | You gave him the *reason* you're worth more than a formula. That was the right move. |
| 3 | You restated **25–30 LPA** on that basis | Correct. |
| 4 | He said **"negotiable, right?"** | **He softened first.** |
| 5 | He said **22 LPA** | Down from your 25–30, up from his own 30%-hike rule. |
| 6 | You raised **relocation and other costs** | Correct — this is your strongest argument. |
| 7 | He said **"we can negotiate it"** | **This is the important one.** |
| 8 | Call disconnected | Unresolved. |

**The single most useful fact in that sequence: he said "22 was max" and then, in the same call, said "we can negotiate it."** Those cannot both be true. **22 is not a hard cap** — it is an opening position. Treat it as one.

### 2.2 Your actual position — and why the relocation argument is now much stronger

You are on **₹13 LPA in Hyderabad, living in your own house on the outskirts.** That changes the arithmetic completely, and it cuts both ways. Be honest with yourself about both halves.

**The case that 22 is a good offer:**

| | |
|---|---|
| **13 → 22 is a ~69% increase** | In absolute market terms, that is a large jump, and it is a real number. Do not dismiss it. |
| **Your current package is low for your skills** | 13 LPA for 3.5 years of data plus shipped agentic AI is under market. The offer corrects that. |
| **It is a genuine step into an AI role** | The career value of the title and the work is real, and hard to price. |

**The case that it is worse than it looks — and this is the argument to make:**

| | Directional estimate |
|---|---|
| **You own your house today** | Zero rent. In Mumbai you rent. |
| **Mumbai rent**, reasonable 1BHK, commutable suburb | **~₹35,000–60,000/month → ₹4.2–7.2 L per year** |
| **Higher cost of living** — transport, food, utilities | **~₹1–2 L per year** on top |
| **You lose remote flexibility** | Real value, hard to price |

**So the honest framing is not "22 is too low." It is:**

> *"22 is a good jump on paper, and I'm not dismissing it. But I'm comparing it to 13 with no rent, in my own house, working remotely. In Mumbai I'd be paying rent for the first time in years. So the real comparison isn't 13 versus 22 — it's 13 with no housing cost versus 22 with ₹5 lakh a year of new housing cost. That's why relocation support matters to me more than the headline number."*

**That is a strong, specific, non-greedy argument.** It uses your actual circumstances, it is verifiable, and it is not a demand.

**One caution:** I am reasoning directionally, not from sourced Mumbai rental data. Check current rents for the areas you'd realistically live in before you quote a figure — a number you can defend beats a range you half-remember.

### 2.3 What is realistic — and my honest confidence level

**I do not have a verified salary band for this role at this company, and I will not invent one.**

| Question | Honest answer |
|---|---|
| Is 22 LPA plausible for this role? | **Yes.** An insurer's Health & Analytics product role at ~12 years total experience sits plausibly in the low-to-mid 20s. |
| Is 22 a hard cap? | **No — he already contradicted himself.** He said "max", then said "we can negotiate it". Treat 22 as an opening, not a ceiling. |
| Does your profile justify asking above it? | **Yes, and you already made the argument.** Regulated healthcare audit **plus** shipped agentic AI is why you were called. |
| Where is a realistic landing? | **₹24–26 LPA** with relocation support is a defensible target; **22 with strong relocation + a dated review** is a reasonable accept. I am inferring from the conversation, not from sourced band data. |
| What is the risk of pushing? | **Low, if you push now and politely.** High if you push after three rounds — by then they expect you to accept. |

**The strategic point:** the time to resolve comp is **now**, not after the loop. Leverage decays with every round you complete.

### 2.4 What to ask for — in priority order

He has already said it's negotiable, so ask for the **total**, and get it in writing:

1. **Relocation support** — a defined amount, or company-arranged accommodation for the first 1–3 months. **This is your priority ask**, and it is the easiest thing for them to grant because it is usually a different budget line from salary.
2. **A joining bonus** — one-time, off-band, and therefore often approvable when the base is not. This is the cleanest way to bridge a base-salary gap.
3. **An early review with a defined number** — *"a performance review at 6 months with a documented revision to ₹X on satisfactory delivery."* A number and a date, or it is worthless.
4. **The grade and title in writing** — *Product Owner* or *Agentic AI*? It matters for your next move.
5. **Clarity on variable pay** — what percentage is performance-linked, and the realistic payout history.

**And re-anchor the base once, using his own inconsistency:** *"You mentioned a 30% hike, which would be around 17, and then 22 — and then said it was negotiable. So I'd like to understand where the band actually sits for this scope, because the role reads broader than a standard analyst band."*

### 2.5 Your walk-away

Decide this **before** the interview. Write it down:

> *"I'll accept 22 if relocation is covered and there's a dated review with a number. If relocation is refused and the base is fixed at 22, I'll ask for 25 again on the strength of the AI work — and I'm willing to stay where I am."*

**You are employed, remote, and own your house.** That is real leverage. You do not need this job — you are evaluating it. Walk in with that posture and you will negotiate better than if you walk in needing it.

**Do not volunteer your current 13 LPA again unless asked directly**, and if asked, state it flatly and move straight to the relocation argument. Let the conversation stay about the value of the role, not the size of your current salary.

---

## §3 — What they are actually building (and the one insight that will land)

### 3.1 Decode the intent behind the words

The JD is written for a **domain owner who can direct technology teams**. The recruiter described **agents that approve/decline/process claims**. The invite says **Agentic AI**. Strip the labels and the actual work is:

> **A decisioning pipeline for health claims** — ingest the claim and its documents, extract the clinical and financial facts, apply policy and medical rules, score risk and fraud, and route each claim either to an automated decision or to a human reviewer — with a defensible explanation and an audit trail for every automated outcome.

That is a **systems + governance** problem with a **domain** wrapper. You have spent three years on the systems and governance half.

### 3.2 The insight to lead with — this is your best single answer

If you say one substantive thing in this interview, say this:

> **"Auto-approval and auto-decline are not the same problem, and treating them as one is the mistake I'd expect a claims automation programme to make.**
>
> **Auto-approval is tractable.** Approving a clean, low-value, in-network, pre-authorised claim within policy limits is a bounded decision. If the system is wrong, you have paid a claim you might have questioned — a cost you can measure, reserve for, and tune the threshold on. That is the straight-through processing win, and it is where the volume is.
>
> **Auto-decline is a different risk class.** A wrong denial is not a cost line — it is a regulatory event, a grievance, possibly an Ombudsman case, and a reputational one. And under Indian health-insurance rules the burden of justifying a rejection sits with the insurer. So a denial should never be a straight-through decision. It should be a *recommendation* with the reasoning surfaced to a human who owns the call, and the evidence attached.
>
> **So I would build the automation to be asymmetric:** automate approvals aggressively behind guardrails, and treat denials as decision-support. That is not a limitation of the technology — it is the correct design for a regulated decision."

**Why this lands:** it shows you understand the domain's risk shape, not just the tech. It reframes you from "AI person" to "person who can be trusted with a regulated decision." And it directly answers the JD's own line about decisions being *"explainable, auditable, and aligned with applicable regulatory requirements."*

### 3.3 The architecture, in words — have this ready to sketch

If they ask how you would approach it, walk the pipeline. Keep each step short:

1. **Intake and classification** — identify the claim type (cashless vs reimbursement), the documents attached, and whether anything mandatory is missing. *Deterministic routing; no model needed for most of it.*
2. **Extraction (IDP/OCR)** — pull structured facts from hospital bills, discharge summaries, and investigation reports: diagnosis, procedure codes, line-item charges, dates, provider identity. *This is where models genuinely help, because document formats vary wildly.*
3. **Policy and coverage engine** — apply the policy contract deterministically: sum insured, sub-limits, room-rent limits, deductibles, co-pay, waiting periods, exclusions, network status. **This must be a rules engine, not an LLM.** Coverage is a contract; a contract is computable, and a probabilistic answer to a contractual question is indefensible in an audit.
4. **Medical necessity and clinical validation** — does the diagnosis justify the procedure, and does the documentation support it? *This is where clinical judgement lives. An LLM can summarise and flag inconsistencies; it should not be the decision-maker.*
5. **Fraud and leakage scoring** — pattern signals: unusual provider billing, repeated claims, mismatched dates, upcoding indicators. *Score and rank; don't adjudicate.*
6. **Routing** — auto-approve / human review / refer for investigation. **No auto-decline.**
7. **Explanation generation** — produce the reason, the rule applied, and the evidence cited, in language a reviewer, a customer, or a regulator can follow. *Generated from the decision trace, never reconstructed by a model after the fact.*
8. **Audit log** — every automated decision stores its inputs, the rules fired, the model versions, and the outcome. Immutable.

**The line that makes this credible:** *"The decision trace has to be the source of the explanation. If you ask a model to explain a decision it didn't structurally make, you get a plausible narrative that isn't the actual reason — and in a regulated decision that is worse than no explanation at all."*

That is a real engineering position, it comes from your own work, and it is the kind of thing a technical interviewer will respect.

---

## §4 — Your fit: map, bridge, and the honest gaps

### 4.1 Where you genuinely match

| JD requirement | Your verified evidence |
|---|---|
| *"Bachelor's degree in Medicine, Dentistry, **Pharmacy**, Nursing…"* | **M. Pharmacy (Pharmaceutical Analysis & Quality Assurance)**, Anurag Group of Institutions (JNTUH), 2012. **You clear the hard filter.** |
| *"Experience in a health insurance company… health claims function… healthcare consulting"* | **9 years at Optum / UnitedHealth Group (2014–2023)** in a regulated US healthcare payer — enrollment quality and audit, CMS compliance, audit-ready documentation. Adjacent, not identical: **say so.** |
| *"Ensure automated claims decisions are explainable, auditable, aligned with regulatory requirements"* | **This is your strongest match.** Your BugAgents promotion gate (four hard criteria; **2 promoted, 34 refused**), the anti-fabrication guard (**8/8 seeded fabrications caught**), and the audit-ledger discipline across your projects. |
| *"Define claims milestones, turnaround times, decision points, escalation triggers, and system controls"* | You have built **escalation and control boundaries** repeatedly — the data-quality agent's bounded retries plus email escalation; BugAgents' per-turn tool-call audit that aborts on a scope violation; budget caps and kill switches. |
| *"Familiarity with Generative AI, intelligent document processing, OCR, machine learning, APIs, rules engines, RPA"* | Genuine, hands-on, shipped. Plus the MCP tool, multi-model routing, evaluation harnesses. |
| *"Work closely with developers, architects, data and testing teams"* | Your data work at Black Piano and Pi Software is exactly this — you have been the person who owns a pipeline and works with the people consuming it. |
| *"Analyzing system performance, exceptions, claims outcomes"* | 18 automated ETL pipelines → BigQuery → Looker Studio; deterministic scoring with zero model calls; exception handling by design. |

### 4.2 The bridge you must get right — Optum

**Do not say "I worked on healthcare claims at Optum." You did not.** You audited **enrollment transactions** for CMS compliance. The moment you imply claims experience and they probe it, you lose the room — and this JD is explicitly for someone who knows claims.

**Say this instead:**

> "Nine years at Optum, auditing Medicare and Medicaid enrollment transactions for CMS compliance. So I'm not a claims adjudicator and I won't pretend to be — that's a gap I'd expect to learn from your medical and claims teams.
>
> What I do bring from those nine years is the discipline the JD is asking for: zero-tolerance pass/fail gates on high-volume federal transactions, every decision traceable to a source document, and documentation that stands up to an external auditor. When you say automated decisions need to be explainable and auditable, that's the muscle I built for nine years before I ever touched a model."

That answer is honest, it converts a gap into a credential, and it sets up §3.2 perfectly.

### 4.3 The gaps — name them before they find them

| Gap | How to say it |
|---|---|
| **No claims adjudication operations experience** | *"I haven't run a claims desk. I've never processed a cashless pre-auth or a repudiation. I'd expect to spend my first weeks with the claims and medical teams learning how decisions are actually made before I propose automating any of them."* |
| **No Indian health-insurance specifics** | *"My regulated-domain experience is US healthcare — CMS. Indian health insurance has its own vocabulary, its own regulator and its own claim norms. I know the concepts; I'd be learning your specifics."* |
| **No TPA experience** | *"I haven't worked inside the insurer–TPA–hospital triangle. I understand how it's structured; I haven't operated in it."* |
| **Never held a Product Owner title** | *"My titles have been Data Analyst. What I've actually done is own systems end to end — define the requirement, build it, set the controls, and hand it to the people who use it. That's the work; the title is new."* |
| **No clinical decision-making authority** | *"I have a pharmacy background, not a clinical practice background. I'd expect medical necessity calls to stay with your medical team, with automation supporting them rather than replacing them."* |

**The posture:** *"I'm not the claims expert you're describing. I'm the person who can build the system the claims expert trusts — and I'd come in knowing exactly which parts I don't know yet."*

### 4.4 The resume — corrected

**You sent the right one.** `Prashanth_Kadasi_Agentic_AI_Engineer_Resume.md` is the agentic variant, it carries your M. Pharmacy, and it already lists the Optum **Claims Associate** role. No correction needed, and no covering note to send.

The one thing it lacks is **product-ownership language** — no roadmap, BRD, user story, sprint or UAT. Close that gap by **speaking** it tomorrow (§7), not by rewriting the resume tonight. Details and the two lines you're underusing: §4A.1.

---

## §4A — Deploying AgentSwarm and BugAgents

### 4A.1 You sent the right resume — now use it properly

`Prashanth_Kadasi_Agentic_AI_Engineer_Resume.md` is **the strongest variant you have for this specific JD**, and here is why:

| What the JD asks for | What that resume already contains |
|---|---|
| *"Bachelor's degree in Medicine, Dentistry, **Pharmacy**, Nursing…"* | **M. Pharmacy (Pharmaceutical Analysis & Quality Assurance)**, JNTUH, May 2012 — in the EDUCATION block |
| *"Experience in a health insurance company… **health claims function**"* | **Optum / UnitedHealth Group, 9 years** — and critically, **"Promoted in March 2016 from Claims Associate (Apr 2014 – Feb 2016)"**. A **Claims Associate** role at a major US health payer is a genuine, literal claims-function title, and it is already on the page. |
| *"Experience working with technology teams on… process automation"* | The whole Black Piano section — pipelines, the self-healing agent, the MCP tool |
| *"Familiarity with Generative AI… will be an advantage"* | Six independent projects with hard numbers |

**So do not swap it.** A data-analyst resume would have been the mistake; this one is the agentic variant with the healthcare spine already in it, and it matches the interview invite title exactly.

**The one thing it does not carry: product-ownership language.** The JD is heavy on roadmaps, BRDs, user stories, acceptance criteria, sprint ceremonies and UAT. Your resume has none of those words. That is the gap to close **verbally** tomorrow — §7 gives you the user stories and the prioritisation answer to do it with. Do not rewrite the resume tonight; prepare to speak the vocabulary instead.

### 4A.1b The two lines on that resume you are underusing

Read your own resume again. Two facts in it are worth more for this interview than anything else you have, and they are buried:

**1. "Claims Associate (Apr 2014 – Feb 2016)".** This is a **claims-function role at a US health payer**, and it is in your canonical profile — so you can say it freely. Say it early and precisely:

> *"I started at Optum as a Claims Associate, then moved into enrollment quality and audit for the rest of my nine years there. So I've been on the claims side of a health payer — though I want to be straight with you: that was US Medicare and Medicaid, and it was sixteen years ago in role terms. I'm not going to pretend that makes me a health-claims operator today. But I'm not arriving with zero context either."*

**Check yourself on this before you use it:** be ready for *"what did you actually do as a Claims Associate?"* If you can describe the work concretely — what came across your desk, what you decided, what the process was — this becomes one of your strongest cards. If you cannot, mention it once, briefly, and move on. **Do not lean on it if you cannot back it up**; that is exactly the kind of claim that collapses under one follow-up.

**2. "M. Pharmacy" is in the EDUCATION block, at the bottom.** The JD's first candidate-profile bullet is a medical-discipline degree. **Say it out loud in your introduction**, because a screener reading top-down may never reach it:

> *"One thing worth flagging up front — I hold an M. Pharmacy, so I clear the medical-discipline requirement in your JD. And I spent nine years at Optum in a US health payer, starting as a Claims Associate and then auditing CMS enrollment transactions."*

That is your opening 30 seconds. It answers the JD's two hardest filters before they ask a question.

### 4A.2 The framing rule — these are your projects, not client work

**AgentSwarm, BugAgents and JobAgents are independent, self-directed projects.** They are not Black Piano or Pi Software deliverables, and your own pipeline enforces that distinction in code because a model got it wrong once. Say it explicitly and early — *"these are my own projects, not client work"* — and it becomes a credibility signal rather than a liability. Let them find it out later and it reads as inflation.

### 4A.3 BugAgents — your strongest parallel to claims adjudication

**Lead with this one.** It is the closest thing in your portfolio to the problem they are describing.

**The verified facts:**

- Two autonomous security-research agents on disjoint targets, with a **report promotion gate** that requires **four conditions to all hold**: scope match, HEAD (commit) match, non-empty reproduction, and evidence files must exist.
- The gate **promoted 2 reports and refused 34** unverified candidates.
- **8 findings** across **14 vulnerability classes** (CWE) — 5 High/Critical, 3 Medium.
- **22 hunt runs / 84 agent turns / 15,317 tool calls** across two harnesses.
- Per-turn tool-call audit: any out-of-scope host or offensive tool **aborts** the agent — and a live run was aborted exactly this way.
- Budget caps and a kill switch; a no-finding verdict is a valid recorded outcome.

**The parallel to state — this is the answer:**

> *"I built a system where an agent produces a candidate outcome, and nothing gets promoted unless four explicit conditions are satisfied and the evidence is on disk. Two passed. Thirty-four were refused. And the refusal count is the number I'd defend hardest — a filter that promotes everything has a refusal count of zero and no verification at all.*
>
> *That is structurally the same problem as automated claims. You have a candidate decision, a set of conditions that must hold, evidence that has to exist, and an outcome that has to be defensible to someone who wasn't there. In my system the failure mode I was designing against was a confident, well-formatted wrong answer that looks exactly like a right one. In claims, that's a wrong approval or a wrong denial. Same shape, higher stakes."*

**Why the 34 refusals land:** it is the opposite of the number a candidate normally presents. It says you understand that a decision system's value is in what it *declines* to decide. For a claims automation programme, that is precisely the instinct they need and rarely find.

### 4A.4 AgentSwarm — the audit-trail answer

**Use this one when they ask about explainability, auditability or governance** — which the JD asks for explicitly.

**The verified facts:**

- An autonomous multi-agent research arena: **34 runs, 35/35 ledger hash chains cryptographically intact.**
- **The ledger lives *outside* the agents' writable directory** — so the audited cannot edit the audit.
- An independent oracle checked every turn for phantom artifacts, fabricated numbers, and asserted verdicts: **0 oracle violations across 1,254 tool calls**, and **0 of 2 self-assessing agents overclaimed.**
- An independent numerical audit verified **22 of 25** quantitative claims correct to the printed digits, located all 5 defects, and returned the verdict **B+ / not publication-grade without that audit.**

**The parallel to state:**

> *"The agents ran unattended and produced output continuously. The interesting engineering was not getting them to produce — it was the layer that decides whether to believe them. Every turn was written to a hash-chained ledger that sits outside the agents' own writable directory, so the thing being audited cannot alter the record of what it did. An independent oracle re-checked every turn for fabricated numbers and phantom artifacts — zero violations across twelve hundred and fifty-four tool calls.*
>
> *For automated claims decisions, that's the audit trail. Not a log file the process writes about itself — a record the process cannot reach."*

**Then volunteer the limitation before they ask** (it is in your ground truth and it makes you more credible, not less):

> *"The honest caveat is that an independent audit of that output graded it B+ — not publication-grade without the numerical audit. I publish that verdict alongside the work. I'd rather ship something whose weaknesses are documented than something that looks clean."*

### 4A.5 JobAgents — the deterministic-gate answer

Use this one when the conversation turns to **cost, scale, or rules versus models**:

> *"I built a job-sourcing pipeline where scoring is pure arithmetic — 22,839 match scores with zero model calls — so only the shortlist ever reaches a model. That's the same discipline I'd want in claims: deterministic rules for anything contractual, and a model only where judgement is genuinely required. A probabilistic answer to a policy-coverage question is indefensible in an audit. And there's a guard that validates generated text against a ground-truth file before anything is written to disk — it catches eight of eight seeded fabrications."*

### 4A.6 What NOT to claim — the guardrails

The interviewer may know this space. Getting caught inflating here costs you the room.

| Do not say | Because |
|---|---|
| That any BugAgents finding was **disclosed, accepted, paid, resolved, or submitted** | Nothing has been submitted. They are submission-ready drafts. |
| The **vendor, program, asset, repository, or vulnerability class** | Withheld pending responsible disclosure. Cite the project and severity counts only. |
| That AgentSwarm's output is **peer-reviewed or publication-grade** | The audit verdict is B+ / not publication-grade without the numerical audit. |
| That you **authored** the AgentSwarm manuscripts | The authors are the agent personas `A001_DarkMatter` / `A002_QuantumCosmos`. You built the system. |
| Any **production users, revenue, adoption or customers** | None exist. These are independent projects. |
| That these were **Black Piano or client work** | They are your own projects. |
| That you have **already applied this to insurance claims** | You have not. The *pattern* transfers; the domain does not. |

**The honest bridge, if they push on relevance:**

> *"I want to be precise about this: I have not built a claims decisioning system. What I have built, three times, is an agent system where an automated outcome is only trusted when it satisfies explicit criteria and leaves evidence behind — and where the escalation boundary is a design decision rather than an afterthought. The logic transfers. Your claims rules, medical logic and policy terms are the part I'd need your teams to teach me, and I'd expect to spend my first weeks learning exactly that."*

### 4A.7 The follow-up questions to expect

| Question | Your answer's spine |
|---|---|
| **"How did you orchestrate the agents?"** | Multi-substrate harnesses across CLI agents, with a shared commons and per-turn recording. The interesting part was not orchestration — it was the verification layer around it. |
| **"How did you evaluate them?"** | An independent oracle re-checking every turn, plus a separate numerical audit of the final output. Never a model grading a model — that rubber-stamps. |
| **"What went wrong?"** | A model violated an explicit prompt rule while producing fluent output. That is why the rule became a code check that can reject the output. *"If it isn't enforced by something that can reject the output, it isn't a rule — it's a suggestion."* |
| **"How would this scale to thousands of claims a day?"** | Deterministic first, model only on the residue. The cost gate has to sit before the model, not around it. My scoring runs free on every item; only the shortlist reaches a model. |
| **"What would you do differently?"** | Instrument the outcome side first. In my own pipeline I measured the top of the funnel precisely and the bottom not at all — I could tell you every score but not whether any of it worked. |
| **"Is any of this employer work?"** | No — independent projects, clearly labelled. My employer work is the pipelines and data-quality systems. |

---

## §4B — The PMP study (2024) — not on the resume, but know how to answer

You spent many days on **PMP exam preparation in 2024, never sat the exam**, and then made a deliberate call: **that's when you started building AI projects instead.** You've decided not to put it on the resume, and that's the right call — unfinished training is not a credential, and listing it invites *"so are you certified?"*, which you'd then have to walk back.

But the JD is heavy on **BRDs, process maps, user stories, acceptance criteria, sprint planning, UAT and defect management**, and your resume carries none of that vocabulary. So the study is worth having *available* if the conversation goes there — as an explanation, not a claim.

### If they ask about delivery or project-management experience

> *"I studied for the PMP in 2024 — didn't sit the exam. I got the structure from it: how scope is defined, how risk is tracked, how change is controlled. Then I made a deliberate choice to put my time into building AI systems instead, which is when I started the agent work. So I have the vocabulary but not the certification, and I wouldn't claim otherwise."*

**Why that answer works:** it is honest, it shows you learn deliberately, and *"I chose where to spend my time — and it's why I have the agent projects"* converts a gap into the origin story of your strongest material. It also pre-empts the follow-up, because you've said the exam wasn't taken before they ask.

**Never say** "PMP certified", "PMP qualified", or "PMP trained" — the last reads as certified to a recruiter skimming, and the correction is worse than the omission. If you mention it at all: *"PMP exam preparation, 2024 — exam not taken."*

**Do not over-explain why you didn't sit it.** One clause is enough. A short answer reads as a decision; a long one reads as an excuse.

### The vocabulary you can legitimately use

Even without the credential, use these words — they are the JD's own language, and they are genuinely yours to use:

scope · milestone · risk register · change control · stakeholder mapping · RACI · critical path · WBS · definition of done · lessons learned

Use them naturally, not as a list. *"I'd want a clear definition of done before we start"* sounds like someone who has thought about delivery — and it is true of you.

---

## §4C — Your best story, and you're not using it

You told the recruiter this, and then moved past it:

> *"I worked on improving my AI skills over the weekend, then implemented these AI skills in my current role to reduce manual work and speed up development. All things taken care of by AI and a proper pipeline — if that fails, I will step in."*

**That is the strongest paragraph you have for this job.** Read it against the JD:

| You said | The JD asks for |
|---|---|
| *"implemented these AI skills in my current role to reduce manual work"* | *"identify automation opportunities and collaborate with technology teams to implement Generative AI and intelligent automation solutions that improve claims accuracy, processing speed…"* |
| *"faster development"* | *"processing speed… operational efficiency"* |
| *"all things taken care of by AI and proper pipeline"* | *"a clear roadmap for the complete automation and digitization of the claims settlement process"* |
| *"**if that fails, I will step in**"* | *"decision points, escalation triggers, and system controls across the claims lifecycle"* |

**You have already done the thing they are hiring someone to do.** Not in claims — but you identified manual work in your own role, built automation for it, ran it in production, and designed the human fallback. That is the job description, executed at small scale, by you, unprompted.

### Say it like this

> *"Something I'd point to that isn't on the CV in this shape. The work I do now involves a lot of repetitive handling. I spent a weekend learning the tooling properly, then built the automation into my actual role — so the routine work runs through a pipeline with the AI handling it, and I step in only when something fails or falls outside what the pipeline can decide.*
>
> *That's the same shape as what you're describing for claims. Automate the routine, keep a human on the exception, and make the boundary between them explicit. I've done it at small scale on my own work; the difference here is the scale and the regulatory stakes — which is exactly why I'd want the claims and medical teams defining the rules before I automate any of them."*

### Why this lands harder than the project list

- **It is employer work, not a side project.** No attribution caveat needed.
- **It is recent and current** — this is your role today, not 2024.
- **It proves you act on a mandate.** They are hiring for someone who sees manual work and automates it. You did that without being asked.
- **The "if that fails, I step in" line is the human-in-the-loop instinct** — and it is the same principle as your best answer in §3.2, which means you can say both and they reinforce each other.

### One caution — keep it modest

Do not inflate this into "I automated my entire function." The honest version is *"I automated the repetitive parts of my own work and kept myself on the exceptions."* That is a smaller claim and a much more credible one. If they ask how much time it saved, use the §4.3 answer: **you do not have a measured figure, and you say so** — then explain the mechanism. An honest "I didn't instrument it" is worth more here than a percentage, because this is an evaluation-minded room.

---

## §5 — Domain fluency: what you must be able to say correctly

The full sourced glossary, lifecycle and regulation are in [health_claims_domain_research.md](health_claims_domain_research.md). **This section is the minimum you must have cold by tomorrow.**

> **Confidence note:** the terms below are my domain knowledge, not sourced citations. They are standard Indian health-insurance usage, but **if a definition matters to a decision, verify it with their team rather than asserting it.** Saying *"my understanding is X — is that how it works here?"* is a strong move, not a weak one.

### 5.1 The ten terms you cannot get wrong

| Term | What it means |
|---|---|
| **Cashless claim** | Treatment at a **network hospital**; the insurer/TPA settles directly with the hospital. The policyholder doesn't pay upfront (beyond non-payables and co-pay). |
| **Reimbursement claim** | The policyholder pays the hospital and claims the amount back from the insurer afterwards. |
| **Pre-authorization (pre-auth)** | Approval obtained **before** planned treatment (or within hours for emergencies) confirming the insurer will cover it. Its absence is a common cause of cashless denial. |
| **TPA** | Third-Party Administrator — an intermediary that administers claims (pre-auth, document collection, processing) on the insurer's behalf. The triangle is **insurer ↔ TPA ↔ hospital**. |
| **Medical scrutiny** | A medically-qualified reviewer assesses whether the diagnosis, treatment and documentation justify the claim. This is where clinical judgement enters. |
| **Adjudication** | The formal decision on a claim — how much is payable, and on what basis. |
| **Repudiation** | Formal **rejection** of a claim. High-stakes, regulator-visible, and the decision you should never automate. |
| **Deduction / disallowance** | Amounts removed from a claim — non-payables, room-rent-limit excess, proportionate deductions. The main source of customer disputes. |
| **Co-pay** | A fixed percentage of the claim the policyholder bears, per the policy terms. |
| **Deductible** | A fixed amount the policyholder pays before the insurer's liability begins. In Indian health policies this often appears as a **per-claim or annual deductible** — distinct from the US meaning where it dominates every claim. |

### 5.2 The terms that show you did the homework

**Room-rent limit** — caps the daily room charge. Crucially, breaching it typically triggers a **proportionate deduction across associated charges**, not just the room difference. This is a classic source of customer complaints and therefore a classic automation-design question.

**Sub-limits** — caps on specific treatments, procedures or disease categories (cataract, maternity, etc.), separate from the overall sum insured.

**Waiting period** — the initial period during which specified conditions aren't covered. **Pre-existing disease (PED)** waiting periods are commonly around 2–4 years.

**Moratorium period** — after a policy has been continuously in force for a defined period (commonly cited as **60 months**), the insurer generally cannot contest the claim on grounds of non-disclosure or misrepresentation, except for proven fraud. *Verify the exact figure with them — this is precisely the kind of rule that governs how much verification your automation must do.*

**Claim TAT** — turnaround time from claim submission to settlement. Regulator-visible and a headline customer metric.

**Settlement ratio** — proportion of claims settled versus repudiated. Publicly quoted by insurers as a trust signal.

**Leakage** — value lost to incorrect or inflated payments (process error, wrong tariff, upcoding, duplicate settlement). **Distinct from fraud**, which is deliberate. Analytics teams are asked to reduce both.

**NCB (No Claim Bonus)** — a benefit for claim-free years, usually a sum-insured increase or premium discount.

**Portability** — moving a health policy between insurers while retaining credit for waiting periods served.

**Ombudsman** — the grievance-redressal route for a policyholder whose claim is rejected or short-settled.

### 5.3 The lifecycle — know the stages and the failure points

**Registration → document verification → medical scrutiny → adjudication → approval/repudiation → settlement → closure.**

For each stage, know **what goes wrong**, because that is what an automation roadmap is built from:

- **Registration** — incomplete intimation, wrong policy linkage, duplicate claim records.
- **Document verification** — missing discharge summary, illegible bills, mismatched dates and names, non-standard formats across thousands of hospitals. **This is the highest-volume manual pain and the best IDP use case.**
- **Medical scrutiny** — reviewer variance, unclear necessity, insufficient clinical detail. **Judgement-heavy; assist, don't replace.**
- **Adjudication** — inconsistent application of policy terms, calculation errors in deductions, rework from disputes.
- **Settlement** — payment delays, reconciliation breaks.
- **Closure** — no feedback loop, so the same exception recurs.

**The point to make:** *"Most of the manual effort sits in document handling and repetitive policy arithmetic. Most of the risk sits in the medical and repudiation decisions. A good roadmap separates those two, because they need completely different kinds of automation."*

### 5.4 The JD's KPIs — and what automation does to each

| KPI | What it measures | Automation effect |
|---|---|---|
| **Claims TAT** | Submission → settlement time | Improves sharply on clean claims; **can worsen** if automation introduces rework on edge cases. |
| **Settlement ratio** | Settled vs repudiated | Should improve if denials are decision-supported rather than automated. |
| **Processing accuracy** | Correct decisions against policy | Improves on arithmetic and rule application; **the risk is confident wrongness** on judgement calls. |
| **Automation rate** | Share of claims handled without human touch | The headline number — and the one most easily gamed. **Say that.** |
| **Leakage** | Value lost to error and over-payment | Falls with better rules and fraud signals. |
| **Rework** | Claims reprocessed after dispute or error | Falls if the first pass is right; **rises** if automation is deployed before the rules are clean. |
| **Cost per claim** | Unit economics | The actual business case. |
| **Customer satisfaction** | NPS / complaint volume | Driven mostly by **denials and deductions**, not speed. |

**The sophisticated point, if you get a chance:** *"Automation rate is the metric most likely to be optimised for its own sake. A high automation rate on approvals is good. A high automation rate on denials is a regulatory problem wearing a KPI. I'd want the automation rate reported split by decision type, not as one number."*

---

## §6 — Likely interview questions, with the spine of each answer

| Question | Your answer's spine |
|---|---|
| **"Tell me about yourself."** | Pharmacy degree → 9 years regulated healthcare audit at Optum → 3.5 years building data pipelines and agentic systems. Then the through-line: *"everything I've built has a component that decides whether to believe the output."* |
| **"What do you know about health claims?"** | Be honest about depth, then show vocabulary: cashless vs reimbursement, pre-auth, medical scrutiny, adjudication, deductions. Then: *"I know the shape of it. I haven't operated it — that's what I'd learn first."* |
| **"How would you automate claims?"** | §3.3, the eight-step pipeline. Land on the rules-engine point and the no-auto-decline point. |
| **"How would you ensure decisions are explainable and auditable?"** | The decision trace is the source of the explanation — never a model narrating a decision it didn't structurally make. Then the BugAgents gate as proof you build this way. |
| **"What's your experience with GenAI?"** | Shipped systems, not experiments. The self-healing agent, the MCP tool, the evaluation harnesses, multi-model routing. Name what broke and what you learned. |
| **"Have you written user stories / BRDs?"** | Be straight: *"Not in a formal PO capacity. I've written specs, requirements and acceptance criteria for systems I built and for the teams consuming them. I'd expect the format to be new and the substance to be familiar."* Then give one concrete example from §7. |
| **"How would you handle disagreement with the medical team?"** | *"They own the clinical call. My job is to make sure the system presents them the evidence they need and doesn't hide it behind a score. If we disagree, it's usually about what the system should decide versus recommend — and that's a design conversation, not a clinical one."* |
| **"What would you do in the first 90 days?"** | 30: sit with claims and medical teams, watch real claims end to end, learn the top ten exception types. 60: quantify where the manual effort concentrates and which decisions are safe to automate. 90: ship one narrow, high-volume, low-risk automation and measure it. **Do not start with denials.** |
| **"Why do you want this role?"** | Honest and forward-looking: it is the intersection of the regulated-data discipline you spent nine years building and the agentic systems you have spent three years building. Do not claim a lifelong passion for claims. |
| **"You're a data analyst — why a product owner role?"** | *"My titles have been analyst. The work has been ownership: I defined what to build, built it, set the controls, and handed it over. That's the job; the title is new to me."* |
| **"Are you comfortable relocating to Mumbai?"** | Answer it directly. If yes, say yes. If conditional, say the condition — this is not the moment to be vague. |
| **"What are your salary expectations?"** | §2. Ask for the full picture first. If pushed: state your number and immediately anchor it to relocation cost, not to greed. |

---

## §7 — Product Owner craft: be able to do this on a whiteboard

If the interview is genuinely for the PO role, this section is the interview.

### 7.1 What they will want to see

- **Requirement translation** — turning "automate claims" into specific, buildable, testable requirements.
- **User stories with acceptance criteria** — in the standard form, with criteria that are actually checkable.
- **Process maps** — current state with the manual interventions marked, and target state with the decision points marked.
- **Prioritisation** — a defensible order, with the reasoning stated.
- **UAT and defect management** — how you know it works before it goes live.
- **Stakeholder management** across Claims, Medical, Ops, Business, Tech — these five have genuinely different incentives and the PO sits between them.

### 7.2 Three user stories you can write on the spot

**Story 1 — document completeness**
> **As a** claims processor, **I want** the system to verify that all mandatory documents are present for a claim type **so that** I don't spend time on claims I'll have to send back.
>
> **Acceptance criteria:**
> - Given a claim of type X, when fewer than the mandatory document set is attached, then the claim is flagged `Incomplete` with the specific missing documents named.
> - Given a claim flagged `Incomplete`, when the missing documents are received, then the claim returns to the queue without manual re-registration.
> - Given a complete claim, when it enters processing, then no completeness flag is raised.
> - Accuracy measured against a labelled set of at least 500 historical claims before go-live.

**Story 2 — policy coverage evaluation**
> **As a** claims processor, **I want** the system to compute coverage, sub-limits, deductibles and co-pay from the policy contract **so that** the payable amount is consistent and traceable.
>
> **Acceptance criteria:**
> - Given a policy and a claim, the system returns the payable amount **and** the rule path that produced it.
> - Given a claim touching a sub-limit or room-rent limit, the system shows the deduction and the clause applied.
> - Given a claim where coverage cannot be determined from available data, the system routes to human review rather than defaulting.
> - On a reconciliation set of settled claims, computed payable matches the settled amount within the agreed tolerance, with every variance explained.

**Story 3 — decision routing and audit**
> **As a** compliance owner, **I want** every automated decision to record its inputs, rules and outcome **so that** we can defend it to a reviewer, a customer or a regulator.
>
> **Acceptance criteria:**
> - Every automated decision stores: claim id, inputs used, rules fired, model versions, decision, timestamp.
> - The record is immutable and retrievable for at least the regulatory retention period.
> - Given a repudiation or short-settlement, the system generates the customer-facing reason **from the recorded rule path**, not from a generated narrative.
> - Given an audit request for any automated decision, the full trace is retrievable within the agreed SLA.

**Note the shape:** every story has a named beneficiary, a *so that* clause stating value, and criteria that are **checkable** — numbers, states, and a measurable threshold. That is what distinguishes a real user story from a wish.

### 7.3 The prioritisation answer

If asked what you would automate first:

> *"Document intake and completeness checking. It is the highest-volume manual effort, the lowest decision risk, it is fully reversible because it only routes work, and it produces the structured data every later stage depends on. Denials come last, if at all — they are the highest-risk decision and they depend on every upstream stage being right. Approvals I'd automate behind thresholds and monitor closely before widening them."*

That answer demonstrates sequencing judgement, which is what a PO is actually hired for.

---

## §8 — Questions to ask them

Ask four or five. These are ordered by how much they tell you.

1. **"Is this role the Product Owner in the JD, or an agentic AI build role — and who would I report to?"** — resolves the title contradiction and tells you what the job is.
2. **"What does the current claims process look like today — how much is manual, and where does it concentrate?"** — reveals whether they have a real baseline or a mandate.
3. **"Is this a new team or an existing one, and how many people are on it?"** — a "new project" with no team is a very different job from joining a function.
4. **"What's the first milestone you'd want delivered, and by when?"** — a scoped ask means a real project; a vague one means an aspiration.
5. **"How do your medical and claims teams feel about automation? Are they partners in this or is it being done to them?"** — the single best predictor of whether this role succeeds. If the answer is "it's being done to them", the job is a political one.
6. **"Who owns the decision when the system and the medical reviewer disagree?"** — tests whether they have thought about governance at all.
7. **"What does the regulatory sign-off path look like for an automated decision?"** — if nobody has an answer, that is your first project.
8. **"How is success measured for this role in the first year?"** — automation rate, TAT, leakage, or something vaguer.
9. **"What's the working model — the JD says Work From Office in Mumbai; is that five days, and is there any flexibility?"** — get it from them, not from the recruiter.
10. **"What's the band and grade for this role, and what does the total package include?"** — ask it on the call, not only in writing.

---

## §9 — Tomorrow: the 24-hour plan

**Tonight (2–3 hours):**
1. Send the clarification message in §1. **Do this first — it is time-sensitive.**
2. Rehearse your **opening 30 seconds** out loud — M. Pharmacy, then Optum Claims Associate → audit, then the verification-layer framing. Five times, until it's natural (§10).
3. Say the §3.2 asymmetry answer **out loud** three times. It is your best 90 seconds.
4. Read §3, §4 and §6 until the *shape* is automatic, not the wording.
5. Read [health_claims_domain_research.md](health_claims_domain_research.md) once — vocabulary and lifecycle only. Do not memorise numbers you cannot source.
6. Decide your walk-away number and write it down (§2.5).
7. Prepare one page of notes. Do not read from a script.

**Morning:**
8. Re-read §5.1 (the ten terms) and §7.2 (the three user stories).
9. Re-read §4.3 (the gaps) so you volunteer them rather than being caught.
10. Check yourself on **"what did you actually do as a Claims Associate?"** — if you can describe it concretely, it's a strong card. If not, mention it once and move on (§4A.1b).
11. Test your setup — camera, mic, connection. Confirm the format and platform.
12. Have the JD open in another window. You will want to reference its exact wording.

**In the room — the five things to remember:**
- **Open with M. Pharmacy and the Optum claims-to-audit line** (§10). It answers the JD's two hardest filters before they ask.
- **Lead with the asymmetry insight** (§3.2). It is the answer that separates you from other candidates.
- **Volunteer the Optum framing** (§4.2) before they probe it.
- **Never claim claims experience you don't have.** You have nine years of regulated audit and three years of agentic systems. That is a strong, true story.
- **Resolve the money question before the end of the conversation,** not after.

---

## §10 — Pocket card

**Say:**
- M. Pharmacy (Pharmaceutical Analysis & QA), 2012 — clears the JD's degree requirement. **Say it out loud — it's buried at the bottom of your resume.**
- Optum, 9 years: started as **Claims Associate (Apr 2014 – Feb 2016)**, then **Enrollment Quality & Audit Representative (CMS Auditor)** auditing Medicare/Medicaid **enrollment** transactions — audit-ready documentation, zero-tolerance gates *(enrollment, not claims adjudication — say so)*
- Self-healing data-quality agent — deterministic lookup, LLM fallback, write-back, 3 retries, **human escalation** *(Black Piano)*
- BugAgents promotion gate — four hard criteria, **2 promoted, 34 refused**; per-turn audit that aborts on a scope violation
- AgentSwarm — **35/35 hash chains intact**, ledger lives *outside* the agents' writable directory; **0 oracle violations across 1,254 tool calls**
- Anti-fabrication guard — **8/8 seeded fabrications caught**; review invariants **0 failures, every check fires when violated**
- 18 automated ETL pipelines → BigQuery → Looker Studio across 18 sectors *(Black Piano)*
- The through-line: *"the component that decides whether to believe the output"*

**Your opening 30 seconds — say this before anything else:**

> *"Two things worth flagging up front. I hold an M. Pharmacy, so I clear the medical-discipline requirement in your JD. And I spent nine years at Optum in a US health payer — I started as a Claims Associate, then moved into enrollment quality and audit. So I've been on the claims side, though I'll be straight that it was US Medicare and Medicaid, and I'm not going to pretend that makes me a health-claims operator today. What I have spent the last three years on is building autonomous agent systems — and the part most relevant to claims isn't the agents, it's the verification layers I had to build around them."*

**Your best story — the one you told the recruiter and then dropped (§4C):**

> *"The work I do now involves a lot of repetitive handling. I spent a weekend learning the tooling properly, then built the automation into my actual role — the routine work runs through a pipeline with the AI handling it, and I step in only when something fails or falls outside what the pipeline can decide. That's the same shape as what you're describing for claims: automate the routine, keep a human on the exception, make the boundary explicit."*

**On money — the two sentences that matter:**

> *"22 is a good jump and I'm not dismissing it. But I'm comparing it to 13 with no rent, in my own house, working remotely — so the real comparison isn't 13 versus 22, it's 13 with no housing cost versus 22 with several lakh a year of new housing cost. That's why relocation support matters to me more than the headline number."*

> *"You mentioned a 30% hike, which would be around 17, and then 22 — and then said it was negotiable. So I'd like to understand where the band actually sits for this scope."*

**The one answer to have ready:**

> *"Auto-approve aggressively behind guardrails; never auto-decline. A wrong approval is a cost you can measure and reserve for. A wrong denial is a regulatory event. So denials stay decision-support, with the reasoning surfaced to a human who owns the call — and the explanation has to come from the recorded decision trace, not from a model narrating a decision it didn't make."*

**Never say:**
- That you have **claims adjudication** or Indian health-insurance operations experience — you don't
- Any title above Data Analyst for held employment
- **"PMP certified" / "qualified" / "trained"** — you prepared and never sat the exam. If it comes up: *"PMP exam preparation, 2024 — exam not taken."*
- Any number not in [../config/profile.md](../config/profile.md)
- Any claim about ICICI Lombard's claim-settlement statistics or financials — you have no sourced figures
- That BugAgents findings were "disclosed", "accepted", "paid", **or "resolved"** — nothing has been submitted
- Any production users, revenue, or adoption claim for your own projects — none exist
- That you **authored** the AgentSwarm manuscripts
- Any specific IRDAI circular number or regulation date you have not verified

**Full forbidden list:** [`outreach_templates.md` §6](outreach_templates.md) — it binds here too.

---

*Companion files: [health_claims_domain_research.md](health_claims_domain_research.md) (claims vocabulary, lifecycle, regulation — sourced) · [icici_lombard_research.md](icici_lombard_research.md) (company intel) · [interview_guide.md](interview_guide.md) (project deep-dives) · [../config/profile.md](../config/profile.md) (binding ground truth)*
