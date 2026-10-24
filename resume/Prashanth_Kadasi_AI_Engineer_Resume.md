# PRASHANTH KUMAR KADASI
**Data Analyst → AI Systems Engineer | Production Data Pipelines, Autonomous Agents & LLM Evaluation**  
Hyderabad, India • +91-9948311964 • kprsnt@live.com  
Portfolio: [kprsnt.in](https://kprsnt.in) • GitHub: [github.com/kprsnt2](https://github.com/kprsnt2) • Hugging Face: [huggingface.co/kprsnt](https://huggingface.co/kprsnt) • LinkedIn: [linkedin.com/in/prashanth-kumar-kadasi-b5281765](https://linkedin.com/in/prashanth-kumar-kadasi-b5281765)

---

### PROFESSIONAL SUMMARY
Data Analyst with 3+ years delivering production data and analytics for US and UK clients, now moving into AI engineering. My paid work is data pipelines and client dashboards; my AI work is independent and self-directed — autonomous agents, LLM fine-tuning, and evaluation harnesses built on my own time. Day-to-day I use Python, SQL, BigQuery, and GCP; my AI stack is FastMCP and multi-agent orchestration with code-enforced verification. I build systems where the architecture, the controls and the audit trail matter more than the demo.
---

### TECHNICAL SKILLS
- **Agentic & LLM:** Multi-Agent Swarms, FastMCP (MCP), Tool/Function Calling, Human-in-the-Loop Escalation, Bounded Autonomy, Agent CI/CD, Agent Evaluation Harnesses, Independent Verifier Design, Hash-Chained Audit Ledgers, RAG
- **LLM & Evaluation:** LoRA/QLoRA Fine-Tuning, Model Evaluation & Steerability, Bias Quantification, Multi-Model A/B Evaluation
- **Languages:** Python (PyTorch, Pandas, NumPy, FastAPI), SQL, Node.js, TypeScript, JavaScript, HTML- **Data:** BigQuery, Looker Studio, Tableau, ETL Orchestration, Data Modeling, Data Quality & Validation, Scheduled Queries, Apps Script, SQLite
- **Infra & Platforms:** GCP, Cloud Run, Docker, GitHub Actions, Vercel, Linux/Bash, Git; Claude 4.x, Gemini 2.5/3.x, GPT-OSS 120B/20B, DeepSeek 4.1, Ollama, OpenRouter
- **Security:** Source-Code Audit, Vulnerability Research, Proof-of-Concept Development, CVSS Scoring, CWE Classification, Bug Bounty Scope Handling

---

### PROFESSIONAL EXPERIENCE

**Black Piano** — *Data Analyst* | Remote  
**Mar 2026 – Present**
- Created end-to-end pipelines for client dashboards, ingesting multi-source sector data into BigQuery and feeding Looker Studio dashboards across 18 sectors.- Produced industry reports (Black Friday, Christmas, sales) and ad-hoc dashboards used by client marketing and sales teams.
- Built a self-healing data-quality agent powered by Gemini: resolves missing brand domains via reference-table lookup with LLM fallback, writes results back to dataset and lookup table, retries 3x, and escalates to humans when unresolved.- Shipped a custom MCP tool letting non-technical marketing and sales staff generate data-grounded blog posts from a one-line prompt, backed by auto-exported Sheets pipelines.
- Engineered an automated AI insights pipeline (ChatGPT) producing weekly market- and sector-level intelligence, auto-published to a client-facing site.

**Pi Software Solutions (Pi – Datametrics)** — *Data Analyst* | Remote  
**Mar 2023 – Feb 2026**
- Built production Python data pipelines (internal `Pi-API` package) for automated BigQuery access across 10+ client dashboards used daily by analytics teams.
- Delivered 30+ analytical reports on US and UK industry trends, standardizing templates.- **Moved from Pi to Black Piano in Mar 2026** — a role change at the same title, not a promotion; Black Piano hires India-based analysts for US and UK clients.

**Optum (UnitedHealth Group)** — *Enrollment Quality & Audit Representative (CMS Auditor)* | Hyderabad, India  
**Apr 2014 – Mar 2023**
- Audited federal enrollment transactions for Centers for Medicare & Medicaid Services (CMS) compliance, producing regulatory documentation and audit-ready discrepancy reports.
- Promoted in Mar 2016 from Claims Associate to Enrollment Quality & Audit Representative based on audit precision and analytical rigor.
- Applied zero-tolerance quality gates to high-volume transaction datasets — the verification discipline I now apply to AI systems.

---

### FEATURED AI & AGENTIC PROJECTS
> **Independent / self-directed work — not employer deliverables.** Built and deployed by me outside employment. None of it is Black Piano or Pi Software client work. Publicly deployed for demonstration; no business metrics claimed.

**MyLocalCLI — Local-First Agentic Coding Assistant** | *Node.js, CLI, 8 providers, 42 tools, 38 skills*  
[Live portal](https://mlc.kprsnt.in) • [npm](https://www.npmjs.com/package/mylocalcli) • [GitHub](https://github.com/kprsnt2/MyLocalCLI)
- Published an open-source terminal coding agent on npm (`mylocalcli`, v4.0.2) — a Claude Code alternative built around local and free-tier models with no telemetry and no paid subscription required.
- Engineered **42 built-in tools** and **38 dynamic skills** across **8 providers** (Ollama and LM Studio local, vLLM self-hosted, OpenRouter and Groq free tiers, NVIDIA NIM, OpenAI, and any OpenAI-compatible endpoint), with **5 specialised sub-agents** (code reviewer, explorer, test generator, refactorer, doc writer).
- Dispatched parallel tool calls concurrently via `Promise.all` instead of sequential blocking, and added provider failover on rate limits, context overflow or connection drops — models are never silently swapped.

**rAsh Score — Multi-Model AI Brand-Visibility Index** | *Next.js, Turso/LibSQL, GitHub Actions, Vercel*  
[Live index](https://rashscore.live)
- Built and operate a live multi-model evaluation platform that queries **4 providers** (ChatGPT, Gemini, Claude, Groq) with standardised prompts and scores **300 tracked brands across 20 industry cohorts** on **4 independent dimensions** — recommendation, sentiment, prominence and factual accuracy.
- Automated daily pipelines via GitHub Actions writing into Turso (LibSQL), with a Next.js dashboard on Vercel; added a multi-agent debate arena and a text-to-SQL analyst chat.

**BugAgents — Two Autonomous Security Research Agents** | *Python/Node, omp + agy CLI orchestration*  
[Live site](https://bug.kprsnt.in)
- Built two agents on disjoint targets hunting real bugs in live bug bounty programs, with a promotion gate that surfaces a report only when the workspace corroborates it (scope match, HEAD match, non-empty reproduction, evidence present).
- Produced **8 findings** across **14 vulnerability classes** (CWE), including **5 High/Critical** and 3 Medium, each with a reproducing proof of concept, pinned commit, and `file:line` citations; **2 submission-ready reports promoted**. *Vendor, asset, and vulnerability-class details withheld pending disclosure; nothing submitted to a program yet.*
- Enforced per-turn tool-call auditing that aborts any agent touching an out-of-scope host or offensive tool — a live run was aborted this way. Ran 15,317 tool calls over 22 hunt runs within a hard budget cap; 8/8 harness tests pass.

**AgentSwarm — Autonomous Multi-Agent Research Arena** | *Node.js, 4 harnesses (agy/omp/pi/step), hash-chained ledger*  
[Live arena](https://agent.kprsnt.in)
- Ran an unattended swarm across **9 research domains** with an independent oracle checking every turn for phantom artifacts, fabricated numbers, and asserted verdicts on undecidable questions: **0 oracle violations across 1,254 tool calls**, **0 of 2 self-assessing agents overclaimed**.
- Kept a hash-chained forensic ledger *outside* the agents' writable directory so the audited cannot edit the audit — **34 runs, 35/35 chains intact**.
- Commissioned an independent numerical audit: **22/25 claims verified exact**; 520 artifacts and 202 finding blogs, suites passing **195/224** on re-run. *Verdict B+; not publication-grade.*
- Wrote two agent-authored cosmology manuscripts in REVTeX, attributed to swarm agents A001_DarkMatter and A002_QuantumCosmos: one is a Zenodo preprint (DOI 10.5281/zenodo.23232189) predicting a falsifiable pulsar-timing signature; the other is a manuscript not yet submitted.

**JobAgents — Automated Job Search Pipeline** | *Python (stdlib only), omp/pi/agy orchestration, SQLite*  
[Live dashboard](https://job.kprsnt.in)
- Built a multi-agent pipeline sourcing **7,613 jobs / 5,854 distinct roles** from **10 sources**, merging **1,759 duplicate postings** via two-layer deduplication.
- Kept scoring deterministic and model-free as a cost gate — **22,839 match scores computed with 0 model calls** — so only top-N candidates reach an LLM; **155** cleared the auto-tailor bar.
- Enforced anti-fabrication in code, not prompts: resume claims are checked against profile ground truth before anything reaches disk, catching **8/8 seeded fabrication classes**.

**AI Eco — 10-Agent Swarm & FastMCP Server** | *Python, FastMCP, living memory, GitHub Actions*  
[Live swarm](https://kprsnt.in/ecosystem) • [Architecture](https://github.com/kprsnt2/kprsnt.in)
- Engineered a **10-agent** swarm running daily CI/CD for repository telemetry, technical-debt pruning, living memory compaction (<4,000 words), and fitness scoring (**83.4%**).
- Deployed a FastMCP server exposing **15+ tools** and 5 resources over JSON-RPC 2.0 and SSE.

**BrandXY — 20B LLM Fine-Tuning & Steerability Research** | *PyTorch, AMD MI300X, LoRA/QLoRA*  
[Model weights](https://huggingface.co/kprsnt/BrandXY-gpt-oss-20b) • [Demo](https://huggingface.co/spaces/kprsnt/brandXY-chat)
- Fine-tuned GPT-OSS-20B on AMD MI300X GPUs to quantify and steer recommendation bias, reaching **76.5% vs 25.5% baseline** under multi-model A/B evaluation. Open weights and demo published.

**Project Awakening — Autonomous Multi-Agent Civilization** | *Multi-agent, FastMCP, SQLite, CI/CD*  
[Live demo](https://kprsnt2.github.io/ac_awakening) • [Code](https://github.com/kprsnt2/ac_awakening)
- Architected an unprompted multi-agent ecosystem spanning **1,441 autonomous turns and 1,553 commits**, sustaining 100% CI/CD integrity through a 330-turn cloud API blackout.

---

### EDUCATION
**Anurag Group of Institutions (JNTUH)** — *M. Pharmacy (Pharmaceutical Analysis & Quality Assurance)* | May 2012
