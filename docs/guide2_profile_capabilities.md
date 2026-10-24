# Senior Resume — Interview Guide 2 of 6: Profile & Core Capabilities

**Covers:** the headline, the PROFILE paragraph, and all six CORE CAPABILITIES groups — every word.

Each entry follows the same shape: **what it claims → how to explain it step by step → likely follow-ups → where it can go wrong → the honest limit.**

---

## §1 — The headline

> **Data Analyst → AI Engineering Leadership | LLM & RAG Systems, Agent Architecture, Verification & Governance**

### What it claims

Three things, and it is important you know exactly which:

1. **"Data Analyst"** — your held title. A fact.
2. **"→ AI Engineering Leadership"** — a **direction**, not a title. The arrow is doing the work: you are moving toward it, not claiming it.
3. **Three technical domains** — LLM/RAG, agent architecture, verification/governance. All three are evidenced by shipped work.

### How to explain it if asked

> *"The headline is a direction, not a title claim. My held titles are Data Analyst at both employers — that's on the resume in the profile section. The arrow points at where the work has been going: the last two years I've been building agent systems and the verification layers around them, which is architecture and governance work rather than analysis."*

### Where it can go wrong

**If you let "AI Engineering Leadership" sound like a held role.** The moment you do, you are claiming a title you do not have, and the profile paragraph directly beneath contradicts you. **The arrow is your protection — use it explicitly if challenged.**

### The honest limit

You have not led a team. "Leadership" here means technical leadership of systems, and you should say so before anyone asks:

> *"To be precise about 'leadership' — I mean ownership of systems and architecture, not people. I haven't had direct reports."*

---

## §2 — The PROFILE paragraph, sentence by sentence

### Sentence 1

> *"Nine years in regulated healthcare operations auditing federal transactions to CMS standards, then three and a half years building the data and AI systems behind client-facing analytics."*

**Step-by-step explanation:**

1. **2014–2023, Optum / UnitedHealth Group.** Audited **Medicare and Medicaid enrollment transactions** for CMS compliance — federal transactions, zero-tolerance quality gates, audit-ready documentation.
2. **2016 promotion** from Claims Associate to Enrollment Quality & Audit Representative, on audit precision.
3. **2023–2026, Pi Software Solutions.** Data Analyst. Python pipelines, BigQuery, 10+ client dashboards, 30+ reports.
4. **2026–present, Black Piano.** Data Analyst. 18 ETL pipelines, the data-quality agent, the MCP tool.

**The critical precision:** it was **enrollment** audit, not **claims adjudication**. Say the distinction before you are asked. Interviewers in insurance and healthcare will know the difference, and blurring it is the fastest way to lose credibility.

> *"To be precise — I audited enrollment transactions, which is the application and eligibility stage. Not claims adjudication. I'd rather be clear about that than let it sound broader than it was."*

### Sentence 2

> *"I own systems end to end — architecture, delivery, controls and the audit trail — and I have spent two years shipping autonomous multi-agent systems where the hard engineering was not making the model produce output but building the layer that decides whether to believe it."*

**This is the strongest sentence on the resume.** Break it into four claims, each of which you can evidence:

| Claim | Evidence |
|---|---|
| **Architecture** | The eight-step design of the data-quality agent (deterministic first, LLM fallback, write-back, bounded retries, escalation); MyLocalCLI's provider abstraction across 8 providers |
| **Delivery** | 18 pipelines in production; MyLocalCLI published on npm at v4.0.2; rAsh Score running daily on GitHub Actions |
| **Controls** | BugAgents' promotion gate (4 criteria); per-turn tool-call auditing that aborts; scope guardrails; budget caps and kill switches |
| **Audit trail** | AgentSwarm's hash-chained ledger living **outside** the agents' writable directory; JobAgents' ground-truth validation before anything reaches disk |

**If asked "what do you mean by the layer that decides whether to believe it?"**

> *"Every one of my systems has a component whose only job is to decide whether an output is trustworthy. In BugAgents it's a promotion gate with four conditions that must all hold — and it refused 34 candidates to promote 2. In JobAgents it's a guard that validates generated text against a ground-truth file before anything is written to disk, and it catches eight of eight seeded fabrications. In AgentSwarm it's a hash-chained ledger outside the agents' writable directory, so the thing being audited can't alter the record of what it did.*
>
> *The reason that matters: a model's output looks the same whether it's right or wrong. Fluency is not correctness. Only the evidence distinguishes them."*

### Sentence 3 — the title paragraph

> *"**Held titles are Data Analyst; the scope has been systems ownership.** I have not had direct reports, and I am precise about that: what I bring is architecture, delivery and governance, not line management."*

**This paragraph is doing deliberate work. Understand why it is there.**

You are being considered for Manager / Senior Manager roles. The risk is that a recruiter reads "Senior Manager" expectations into your application and then discovers the gap at offer stage. **By stating it yourself, you control the frame** — and you convert a potential disqualification into evidence of precision.

**How to use it:**

> *"I put that on the resume deliberately. The roles I'm being approached for are at manager level, and I'd rather be upfront than have it surface later: I've never had direct reports. What I have is architecture, delivery and governance ownership. If the role requires line management from day one, that's a real conversation — and I'd rather have it now."*

**Where it can go wrong:** saying it **apologetically**. It is not a confession, it is a boundary. Say it flatly and move on.

---

## §3 — CORE CAPABILITIES: the six groups

Interviewers screen from this block. Each line must be defensible in one sentence plus one example.

### 3.1 AI & Agent Architecture

> *multi-agent orchestration, RAG, tool/function calling, MCP tooling, multi-model routing and failover, bounded autonomy, human-in-the-loop escalation design*

| Term | Your one-line defence | Your example |
|---|---|---|
| **Multi-agent orchestration** | Running several agents with distinct roles on a shared problem, with a coordination and verification layer between them | **AgentSwarm** — a research arena with an independent oracle checking every turn; **BugAgents** — two agents on disjoint targets |
| **RAG** | Retrieval-augmented generation — grounding a model's output in retrieved source material rather than relying on its parameters | The **MCP tool** at Black Piano: content is generated from auto-exported Sheets data, not from the model's memory. The engineering was grounding, not generation |
| **Tool/function calling** | Giving a model a defined set of callable functions with typed arguments, so its actions are structured rather than prose | **MyLocalCLI** — 42 built-in tools the agent invokes; the agent decides which to call and with what arguments |
| **MCP tooling** | Model Context Protocol — a standard interface for exposing tools and resources to a model | Built a **custom MCP tool** at Black Piano; **AI Eco** exposes 15+ MCP tools and 5 resources over JSON-RPC 2.0 and SSE |
| **Multi-model routing and failover** | Sending work to different providers by rule, and degrading gracefully when one fails | **rAsh Score** queries 4 providers; **MyLocalCLI** fails over between 8 providers on rate limits, context overflow and connection drops |
| **Bounded autonomy** | Agents that act without a human, within explicit limits that cannot be exceeded | **AI Eco** — living memory bounded under 4,000 words; BugAgents — hard budget cap with a kill switch |
| **Human-in-the-loop escalation design** | Defining the exact conditions under which a human must decide, and making that path reliable | The **data-quality agent** — 3 bounded retries, then email escalation. The system is autonomous on the routine and explicitly non-autonomous on the residue |

**The follow-up you will get: "What's the difference between RAG and fine-tuning, and when do you use which?"**

> *"RAG when the knowledge changes or must be traceable to a source — you retrieve at query time, so the answer can cite where it came from, and you can update the corpus without retraining. Fine-tuning when you want to change behaviour or style rather than inject facts — I did that with BrandXY, a LoRA fine-tune of GPT-OSS-20B, to steer how the model scored brands. If the requirement is 'the answer must be defensible against a document', that's RAG. If it's 'the model must behave differently', that's tuning."*

### 3.2 Verification & Governance

> *evaluation harnesses, independent verifier design, evidence gates, hash-chained audit ledgers, scope guardrails, budget enforcement, explainable decision traces*

**This is your differentiator. Most AI engineers cannot speak to this block at all.**

| Term | Your one-line defence | Your example |
|---|---|---|
| **Evaluation harnesses** | A repeatable structure for testing whether a system's output is correct, independent of the system that produced it | **rAsh Score** — standardised prompts across 4 providers, scoring on 4 independent dimensions; **AgentSwarm's** independent oracle |
| **Independent verifier design** | A checker that is not the thing being checked, and that can reject output | The **promotion gate** in BugAgents — checked against the filesystem and the target's own state, never against the agent's summary of them |
| **Evidence gates** | A hard condition that must be satisfied before an output is accepted | Four conditions in BugAgents: scope match + HEAD match + non-empty reproduction + evidence files exist |
| **Hash-chained audit ledgers** | A tamper-evident record: each entry hashes the previous one, so altering history breaks the chain | **AgentSwarm** — 34 runs, 35/35 chains intact. The ledger lives **outside** the agents' writable directory |
| **Scope guardrails** | Explicit boundaries an agent cannot cross, enforced rather than requested | BugAgents' per-turn tool-call audit — any out-of-scope host or offensive tool **aborts** the agent |
| **Budget enforcement** | Hard caps on spend, turns and wall-clock time | `MAX_SPEND_USD`, `MAX_TURNS_PER_AGENT`, `MAX_WALL_CLOCK_MINUTES`, and a `STOP` file that halts at the next turn boundary |
| **Explainable decision traces** | The recorded reason a decision was made, from which an explanation is generated — not reconstructed afterwards | The design principle in the APPROACH section (Guide 5) |

**The follow-up: "How do you know your checker works?"**

> *"I validate it by falsification, not spot-checking. In JobAgents I deliberately violated every review invariant and asserted each one fires — zero failures. A checker that only ever returns pass is worthless, because it manufactures confidence in a verdict nobody verified. So proving the opposite is the only useful test."*

### 3.3 Delivery & Engineering

> *Python (FastAPI, Pandas, PyTorch), SQL, Node.js, TypeScript, REST APIs, Docker, GitHub Actions, CI/CD*

**Be precise here — do not overclaim depth.**

- **Python** — your primary language. FastAPI in agent work; Pandas for data; PyTorch for the BrandXY fine-tune. **If asked your level: you are strong on architecture and reasoning, and you use AI-assisted tooling heavily for volume code.** Say that — it is in your resume's AI-Assisted Delivery line and it is consistent.
- **SQL** — daily use across 3.5 years. Window functions, CTEs, joins, aggregation, query optimisation.
- **Node.js / TypeScript** — MyLocalCLI is Node.js; rAsh Score is Next.js/TypeScript. Real, shipped.
- **REST APIs** — the `Pi-API` package, MyLocalCLI's provider layer, rAsh Score's endpoints.
- **Docker** — in your verified skills; used for containerised deployment.
- **GitHub Actions / CI/CD** — rAsh Score runs daily pipelines on it; AI Eco runs scheduled workflows; Project Awakening held 100% CI integrity through a 330-turn API blackout.

**The follow-up: "Rate yourself in Python."**

> *"I can read and reason about Python, and I understand the architecture of everything I've built — the pipeline design, the data model, the control flow, the failure modes. Where I'm weaker is writing large volumes of code from scratch unaided, and debugging unfamiliar code quickly. I use agent harnesses heavily for that, which is on the resume. I'd rather tell you that than have you find out in week two."*

**Do not claim senior-level Python engineering you cannot demonstrate.** The gap becomes visible in weeks, and a failing project is where it gets attributed to the hire.

### 3.4 Data Platform

> *BigQuery, GCP, Cloud Run, Looker Studio, ETL orchestration, data modelling, data quality and validation*

**This block is entirely employer work and fully defensible.** Use it when the conversation turns practical.

| Term | Evidence |
|---|---|
| **BigQuery** | 18 pipelines at Black Piano; `Pi-API` package at Pi Software |
| **GCP** | The platform across both employers; Cloud Run for deployment |
| **Looker Studio** | The dashboard layer for 18 sectors |
| **ETL orchestration** | 18 automated pipelines; scheduled queries; Google Apps Script |
| **Data modelling** | Multi-source ingestion into a warehouse model serving dashboards |
| **Data quality and validation** | The self-healing agent; zero-tolerance gates from Optum |

**The follow-up: "How would you optimise a slow BigQuery query?"**

> *"Partitioning and pruning first — most slow queries are scanning more than they need. Then pushing filters down rather than filtering after the join, avoiding `SELECT *` so you are not paying to read columns you discard, and materialising expensive intermediate results if the same aggregation runs repeatedly. And for a scheduled dashboard, pre-aggregating on a schedule beats running the same heavy query on every page load."*

### 3.5 AI-Assisted Delivery

> *Antigravity, Claude Code, DeepSeek Harness, omp, pi, agy; multi-harness orchestration with controlled comparison across substrates*

**This line is deliberate and you should own it without apology.** See Guide 1 §5 for the full answer, but the short version:

> *"I use agent harnesses as development tooling, the same way I'd use an IDE. What I own is the design and the decisions — the architecture, the failure modes, the controls. Where I'm weaker is writing large amounts of code unaided. And the part I'd point at is that I know where these tools fail, because I've built the verification layers around them."*

**"Multi-harness orchestration with controlled comparison across substrates"** — this means you ran the same task across different harnesses to compare them, holding variables constant. Evidence: **AgentSwarm** ran on 4 harnesses (agy, omp, pi, step); **pRash** benchmarked 6 autonomous coding CLIs over 2 rounds.

**Why this is a skill and not just tool usage:** running the same workload across substrates, holding the model constant to isolate the CLI and vice versa, is an experimental design discipline. Say it that way.

### 3.6 Domain

> *CMS compliance auditing, regulatory documentation, zero-tolerance quality gates, audit readiness*

**This is the block that makes you unusual.** Most AI engineers have no regulated-domain experience at all.

> *"Nine years auditing federal enrollment transactions to CMS standards. Every decision had to be traceable to a rule and defensible to an external auditor, with zero-tolerance quality gates on high-volume data. That's the same requirement the job descriptions put on automated decisions — explainable, auditable, aligned with regulatory requirements. I've spent nine years being the person who had to defend a decision after the fact."*

**The bridge line, if the role is in insurance or healthcare:**

> *"Different regulator, same discipline. CMS audit taught me that a number you can't trace to a source document isn't a number, it's an assertion. I build systems with that assumption."*

---

## §4 — Practice set for this guide

Answer each in 90 seconds, out loud, with the four-beat framework.

| # | Question |
|---|---|
| 1 | Walk me through your headline — what does "AI Engineering Leadership" mean? |
| 2 | Tell me about yourself. *(Use the §3 positioning from Guide 1.)* |
| 3 | You've never managed a team. How is this senior? |
| 4 | What does "the layer that decides whether to believe it" mean? |
| 5 | RAG or fine-tuning — when do you use which? |
| 6 | How do you know your checker actually works? |
| 7 | Rate yourself in Python. |
| 8 | How would you optimise a slow BigQuery query? |
| 9 | You used AI to build these. Is that a problem? |
| 10 | What does nine years of CMS audit give you in an AI role? |

**Score yourself 1–5 on:** Did I answer first? Did I state my criteria? Did I give one concrete example with numbers? Did I name a boundary or limitation? **Below 4 on the last two is where this level is won or lost.**

---

*← Guide 1: Framework · Guide 3: Professional Experience →*
