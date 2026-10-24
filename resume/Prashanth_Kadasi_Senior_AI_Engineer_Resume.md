# PRASHANTH KUMAR KADASI
**Data Analyst → AI Engineering Leadership | LLM & RAG Systems, Agent Architecture, Verification & Governance**  
Hyderabad, Telangana, India • +91-9948311964 • kprsnt@live.com  
Portfolio: [kprsnt.in](https://kprsnt.in) • GitHub: [github.com/kprsnt2](https://github.com/kprsnt2) • Hugging Face: [huggingface.co/kprsnt](https://huggingface.co/kprsnt) • LinkedIn: [linkedin.com/in/prashanth-kumar-kadasi-b5281765](https://linkedin.com/in/prashanth-kumar-kadasi-b5281765)

---

### PROFILE

Nine years in regulated healthcare operations auditing federal transactions to CMS standards, then three and a half years building the data and AI systems behind client-facing analytics. I own systems end to end — architecture, delivery, controls and the audit trail — and I have spent two years shipping autonomous multi-agent systems where the hard engineering was not making the model produce output but building the layer that decides whether to believe it.

**Held titles are Data Analyst; the scope has been systems ownership.** I have not had direct reports, and I am precise about that: what I bring is architecture, delivery and governance, not line management.

---

### CORE CAPABILITIES

- **AI & Agent Architecture** — multi-agent orchestration, RAG, tool/function calling, MCP tooling, multi-model routing and failover, bounded autonomy, human-in-the-loop escalation design
- **Verification & Governance** — evaluation harnesses, independent verifier design, evidence gates, hash-chained audit ledgers, scope guardrails, budget enforcement, explainable decision traces
- **Delivery & Engineering** — Python (FastAPI, Pandas, PyTorch), SQL, Node.js, TypeScript, REST APIs, Docker, GitHub Actions, CI/CD
- **Data Platform** — BigQuery, GCP, Cloud Run, Looker Studio, ETL orchestration, data modelling, data quality and validation
- **AI-Assisted Delivery** — Antigravity, Claude Code, DeepSeek Harness, omp, pi, agy; multi-harness orchestration with controlled comparison across substrates
- **Domain** — CMS compliance auditing, regulatory documentation, zero-tolerance quality gates, audit readiness

---

### PROFESSIONAL EXPERIENCE

**Black Piano** — *Data Analyst* | Remote  
**Mar 2026 – Present**

- **Own the pipeline layer end to end** for client-facing analytics: **18 automated ETL pipelines** feeding BigQuery → Looker Studio dashboards across **18 industry sectors**, from source ingestion and scheduling through to the dashboard.
- **Designed and shipped a self-healing data-quality agent** (Gemini) that resolves missing brand domains autonomously — deterministic reference-table lookup first, LLM fallback for the long tail, write-back to both the dataset and the lookup table so resolutions persist. Bounded at **3 retries**, then **email escalation to a human**. The write-back converts a recurring model call into a one-time cost plus a free table lookup, so the system gets cheaper the longer it runs.
- **Built a custom MCP tool** enabling non-technical marketing and sales teams to generate publication-ready, data-grounded content from a one-line prompt, backed by auto-exported Google Sheets pipelines. The engineering was grounding, not generation.
- **Engineered an automated AI insights pipeline** (ChatGPT) producing weekly market- and sector-level intelligence, auto-published to a client-facing site.
- **Applied AI-assisted development to my own delivery** — using agent harnesses to compress routine work and shorten build cycles, with a human decision point wherever the pipeline cannot resolve an outcome.

**Pi Software Solutions (Pi – Datametrics)** — *Data Analyst* | Remote  
**Mar 2023 – Feb 2026**

- Built production **Python data pipelines** (internal `Pi-API` package) for automated BigQuery access across **10+ client dashboards** used by US and UK teams.
- Delivered **30+ analytical reports** on US and UK industry trends; standardised reporting templates and reconciled source discrepancies across concurrent client engagements.

**Optum (UnitedHealth Group)** — *Enrollment Quality & Audit Representative (CMS Auditor)* | Hyderabad, India  
**Apr 2014 – Mar 2023**

- Audited federal enrollment transactions for **Centers for Medicare & Medicaid Services (CMS)** compliance, producing regulatory documentation, statutory compliance checks and audit-ready discrepancy reports.
- Applied **zero-tolerance quality gates** to high-volume transaction datasets — every decision traceable to a rule and defensible to an external auditor. This is the discipline I now build into automated systems.
- Promoted in Mar 2016 from Claims Associate on audit precision and analytical rigour.

---

### SELECTED SYSTEMS

> **Independent, self-directed work — not employer deliverables.** Built and operated on my own time, publicly deployed. No users, revenue or adoption claimed.

**MyLocalCLI — Local-First Agentic Coding Assistant** | *Node.js, CLI, 8 providers*  
[Portal](https://mlc.kprsnt.in) • [npm](https://www.npmjs.com/package/mylocalcli) • [GitHub](https://github.com/kprsnt2/MyLocalCLI)
- Published an open-source terminal coding agent on npm (**v4.0.2**) — a Claude Code alternative built around local and free-tier models with no telemetry.
- **42 built-in tools**, **38 dynamic skills**, **8 providers** (Ollama, LM Studio, vLLM, OpenRouter, Groq, NVIDIA NIM, OpenAI, custom), **5 specialised sub-agents**.
- Parallel tool dispatch via `Promise.all` instead of sequential blocking; provider failover on rate limits, context overflow and connection drops, with models never silently swapped.

**rAsh Score — Multi-Model AI Brand-Visibility Index** | *Next.js, Turso/LibSQL, GitHub Actions, Vercel*  
[Live](https://rashscore.live)
- Built and operate a live multi-model evaluation platform querying **4 providers** (ChatGPT, Gemini, Claude, Groq) with standardised prompts, scoring **300 tracked brands across 20 industry cohorts** on **4 independent dimensions** — recommendation, sentiment, prominence, factual accuracy.
- Daily automated pipelines writing into Turso (LibSQL), surfaced through a Next.js dashboard on Vercel; includes a multi-agent debate arena and a text-to-SQL analyst chat.

**BugAgents — Evidence-Gated Autonomous Security Research** | *Python/Node, multi-harness orchestration*  
[Live](https://bug.kprsnt.in)
- Built the **report promotion gate** that separates a corroborated finding from a plausible write-up: **scope match + HEAD match + non-empty reproduction + evidence files must exist**. It **promoted 2 reports and refused 34** unverified candidates — the refusal count is the control working.
- Enforced **per-turn tool-call auditing** that aborts any agent touching an out-of-scope host or offensive tool; a live run was aborted exactly this way. **22 hunt runs / 84 agent turns / 15,317 tool calls** within a hard budget cap.
- Produced **8 findings across 14 vulnerability classes** (CWE). *Vendor, asset and vulnerability-class details withheld pending disclosure; nothing submitted to a program.*

**AgentSwarm — Auditable Multi-Agent Research Arena** | *Node.js, 4 harnesses, hash-chained ledger*  
[Live](https://agent.kprsnt.in)
- Ran **34 unattended runs with all 35 ledger hash chains intact**. The ledger lives **outside the agents' writable directory**, so the audited cannot edit the audit.
- Independent oracle checked every turn: **0 violations across 1,254 tool calls**, and **0 of 2 self-assessing agents overclaimed**.
- Commissioned an independent numerical audit: **22 of 25 quantitative claims verified exact**, verdict **B+ / not publication-grade without that audit** — published alongside the work rather than hidden.

**JobAgents — Deterministic Sourcing & Anti-Fabrication Pipeline** | *Python (stdlib only), SQLite*  
[Live](https://job.kprsnt.in)
- Sourced **7,613 jobs / 5,854 distinct roles** from **10 sources** across **334 companies**, merging **1,759 duplicate postings** via two-layer dedupe.
- Kept scoring **deterministic and model-free as a cost gate** — **22,839 match scores with 0 model calls** — so only the top-N reach an LLM.
- Enforced anti-fabrication **in code, not prompts**: generated claims are validated against a ground-truth file before anything reaches disk, catching **8/8 seeded fabrication classes**.

**Also shipped:** AI Eco (10-agent swarm, FastMCP server, <4,000-word bounded memory), BrandXY (GPT-OSS-20B LoRA fine-tune, **76.5% vs 25.5%** baseline), Project Awakening (**1,441 autonomous turns**, 100% CI integrity through a 330-turn API blackout), mSeat (18,000+ candidate allocation simulator, validated within **73 ranks** of official cutoffs).

---

### APPROACH — what I actually bring

**Verification before autonomy.** Every system above has a component that decides whether to believe the output. On a regulated decision that is not a feature, it is the design: automated approvals are tractable, automated denials are a regulatory event, and the explanation has to come from the recorded decision trace rather than a model narrating a decision it did not make.

**Deterministic where it is contractual, model-based only where judgement is required.** Cost gates sit before the model, not around it.

**Bounded autonomy with an explicit human boundary.** Retries are capped, escalations are defined, budgets and kill switches exist, and a no-result outcome is a valid recorded result.

**Disclosure over polish.** Where a result is weak I publish the weakness — a B+ audit verdict, 34 refused candidates, a self-audit that found its own headline result circular. A system whose limits are documented is more useful than one that looks clean.

---

### EDUCATION
**Anurag Group of Institutions (JNTUH)** — *M. Pharmacy (Pharmaceutical Analysis & Quality Assurance)* | May 2012
