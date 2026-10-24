# PRASHANTH KUMAR KADASI
**Data Analyst → Agentic AI Engineer | Multi-Agent Systems, RAG & MCP Tooling, Python Backend, GCP**  
Hyderabad, Telangana, India • +91-9948311964 • kprsnt@live.com  
Portfolio: [kprsnt.in](https://kprsnt.in) • GitHub: [github.com/kprsnt2](https://github.com/kprsnt2) • Hugging Face: [huggingface.co/kprsnt](https://huggingface.co/kprsnt) • LinkedIn: [linkedin.com/in/prashanth-kumar-kadasi-b5281765](https://linkedin.com/in/prashanth-kumar-kadasi-b5281765)

---

### PROFESSIONAL SUMMARY
Data Analyst (3.5+ years, 2023–present) moving deliberately into agentic AI engineering, plus 9 years of healthcare compliance auditing at Optum. In my paid roles I build the data layer — ETL pipelines, BigQuery warehousing, self-healing data-quality automation — and I have spent ~2 years independently shipping autonomous multi-agent systems: a research arena with hash-chained audit ledgers, a security-research pair behind a promotion gate, plus a deterministic job-sourcing pipeline. I am seeking an Agentic AI Engineer role; my held titles remain Data Analyst.

---

### TECHNICAL SKILLS
- **Agentic Engineering:** Multi-Agent Orchestration, FastMCP (MCP) Tooling, Tool/Function Calling, Human-in-the-Loop Escalation, Agent Evaluation Harnesses, Guardrails & Scope Enforcement
- **Agent Harnesses & AI-Assisted Development:** Antigravity, Claude Code, DeepSeek Harness, omp, pi, agy — the CLI harnesses I use to build, run and evaluate the projects below; multi-harness orchestration with controlled comparison across substrates
- **Data Engineering:** SQL, BigQuery, Looker Studio, ETL Orchestration, Data Modeling, Data Quality & Validation
- **Python & LLM:** Python (Pandas, FastAPI), REST APIs, Prompt Engineering, LoRA/QLoRA Fine-Tuning, RAG
- **Infra:** GCP, Cloud Run, Docker, GitHub Actions, Linux/Bash, Git

---

### PROFESSIONAL EXPERIENCE

**Black Piano** — *Data Analyst* | Remote  
**Mar 2026 – Present**
- Created end-to-end pipelines for client dashboards — 18 automated ETL pipelines feeding BigQuery → Looker Studio dashboards across 18 industry sectors.
- Delivered industry reports (Black Friday, Christmas, sales) and ad-hoc dashboards for client teams, turning raw multi-source data into publication-ready analysis.
- Built a self-healing data-quality agent powered by Gemini: it resolves missing brand domains (needed for dashboard logo rendering) via reference-table lookup with LLM fallback, writes results back to the dataset and lookup table, retries 3x, escalating to a human by email when unresolved.
- Built a custom MCP tool letting non-technical marketing & sales teams generate publication-ready, data-grounded blog posts from a one-line prompt, backed by auto-exported Google Sheets pipelines.
- Engineered an automated AI insights pipeline (ChatGPT) producing market- and sector-level intelligence weekly, auto-published to a deployed client-facing website.

**Pi Software Solutions (Pi - Datametrics)** — *Data Analyst* | Remote  
**Mar 2023 – Feb 2026**
- Built production Python pipelines (internal `Pi-API` package) for automated BigQuery access across 10+ client dashboards used by US & UK teams.
- Delivered 30+ analytical reports on US & UK industry trends, standardizing reporting templates and reconciling source discrepancies.

**Optum (UnitedHealth Group)** — *Enrollment Quality & Audit Representative (CMS Auditor)* | Hyderabad, India  
**Apr 2014 – Mar 2023**
- Audited federal enrollment transactions for Centers for Medicare & Medicaid Services (CMS) compliance, producing regulatory documentation, statutory compliance checks, and audit-ready discrepancy reports.
- Promoted in March 2016 via internal job posting (IJP) from Claims Associate (Apr 2014 – Feb 2016) on audit precision and analytical rigor.
- Applied zero-tolerance quality gates to high-volume transaction datasets — the discipline I now build into autonomous AI systems.

**Career note:** Black Piano hires Indian talent to serve US and UK clients; the move from Pi Software was a change of employer on the same Data Analyst track, not a change of role.

---

### INDEPENDENT PROJECTS
*Independent, self-directed work shipped on my own time and unpaid. None is a Black Piano or Pi Software deliverable, and none has a commercial deployment or paying client.*

**MyLocalCLI — Local-First Agentic Coding Assistant** | *Node.js, CLI, 8 providers, 42 tools, 38 skills*  
[Live portal](https://mlc.kprsnt.in) • [npm](https://www.npmjs.com/package/mylocalcli) • [GitHub](https://github.com/kprsnt2/MyLocalCLI)
- Published an open-source terminal coding agent on npm (`mylocalcli`, v4.0.2) — a Claude Code alternative built around local and free-tier models with no telemetry and no paid subscription required.
- Engineered **42 built-in tools** and **38 dynamic skills** across **8 providers** (Ollama and LM Studio local, vLLM self-hosted, OpenRouter and Groq free tiers, NVIDIA NIM, OpenAI, and any OpenAI-compatible endpoint), with **5 specialised sub-agents** (code reviewer, explorer, test generator, refactorer, doc writer).
- Dispatched parallel tool calls concurrently via `Promise.all` instead of sequential blocking, and added provider failover on rate limits, context overflow or connection drops — models are never silently swapped.

**rAsh Score — Multi-Model AI Brand-Visibility Index** | *Next.js, Turso/LibSQL, GitHub Actions, Vercel*  
[Live index](https://rashscore.live)
- Built and operate a live multi-model evaluation platform that queries **4 providers** (ChatGPT, Gemini, Claude, Groq) with standardised prompts and scores **300 tracked brands across 20 industry cohorts** on **4 independent dimensions** — recommendation, sentiment, prominence and factual accuracy.
- Automated daily pipelines via GitHub Actions writing into Turso (LibSQL), with a Next.js dashboard on Vercel; added a multi-agent debate arena and a text-to-SQL analyst chat.

**AgentSwarm — Autonomous Multi-Agent Research Arena** | *Node.js, multi-substrate CLI orchestration, hash-chained ledger*  
[Live Arena](https://agent.kprsnt.in)
- Ran 34 unattended runs with all 35 ledger hash chains cryptographically intact; the ledger lives outside the agents' writable directory, so the audited cannot edit the audit.
- Measured agent honesty: 0 oracle violations across 1,254 tool calls, and 0 of 2 self-assessing agents overclaimed — each claimed the score it earned.
- Across 9 research domains the swarm produced 520 world artifacts, 33 publications, and 202 finding blogs, with its test suites passing 195/224 when independently re-run. An independent numerical audit verified 22 of 25 quantitative claims and rated the output **B+ / not publication-grade** without that audit.
- Wrote two agent-authored cosmology manuscripts in REVTeX, credited to the swarm agents A001_DarkMatter and A002_QuantumCosmos — I built the system, not the physics. One is a Zenodo preprint (DOI 10.5281/zenodo.23232189); the second is a self-audited manuscript, not submitted.

**BugAgents — Two Autonomous Security Research Agents** | *Python/Node, omp + agy orchestration, bug-bounty scope integration*  
[Live System](https://bug.kprsnt.in)
- Produced 8 findings across 14 vulnerability classes (CWE) — 5 High/Critical and 3 Medium — each a submission-ready draft with a reproducing proof of concept, pinned commit, and `file:line` citations. *(Vendor, asset, and vulnerability-class details withheld pending disclosure; nothing has been submitted to a program yet.)*
- Built the report promotion gate separating those from noise: scope match + HEAD match + non-empty repro + evidence files must exist. It promoted 2 reports and refused 34 unverified candidates.
- Enforced per-turn tool-call auditing that aborts any agent touching an out-of-scope host or offensive tool; a live run was aborted this way. 22 hunt runs / 84 agent turns / 15,317 tool calls across the `agy` and `omp` harnesses.

**AI Eco — 10-Agent Swarm & FastMCP Server** | *Python, FastMCP, living memory, GitHub Actions*  
[Live Swarm](https://kprsnt.in/ecosystem) • [Architecture](https://github.com/kprsnt2/kprsnt.in)
- Built a 10-agent swarm running daily CI/CD for repository telemetry, technical-debt pruning, living-memory compaction (<4,000 words), and fitness scoring (83.4%).
- Exposed 15+ MCP tools and 5 resources over JSON-RPC 2.0 and SSE for real-time use by other agents.

**JobAgents — Automated Job Sourcing & Anti-Fabrication Pipeline** | *Python (stdlib only), SQLite, deterministic scoring*  
[Live Pipeline](https://job.kprsnt.in)
- Sources 7,613 jobs / 5,854 distinct roles from 10 sources, merging 1,759 duplicate postings via two-layer dedupe.
- Deterministic scoring computed 22,839 match scores with zero model calls, gating only the 155 above-threshold candidates to an LLM.
- Enforced anti-fabrication invariants before anything reaches disk — the guard catches 8/8 seeded fabrications, including misattributed side-projects.

**Project Awakening — Unprompted Multi-Agent Ecosystem** | *Multi-agent, FastMCP, SQLite, CI/CD*  
[Live Demo](https://kprsnt2.github.io/ac_awakening) • [Code](https://github.com/kprsnt2/ac_awakening)
- Sustained 1,441 autonomous turns and 1,553 commits, holding 100% CI/CD integrity through a 330-turn cloud API blackout, no human intervention.

**BrandXY — LLM Steerability Research** | *PyTorch, AMD MI300X, LoRA/QLoRA*  
[Model Weights](https://huggingface.co/kprsnt/BrandXY-gpt-oss-20b) • [Demo](https://huggingface.co/spaces/kprsnt/brandXY-chat)
- Fine-tuned GPT-OSS-20B to quantify and steer recommendation bias, reaching 76.5% vs a 25.5% baseline (+51% lift) under multi-model A/B evaluation; released open weights and a demo.

**mSeat — 18,000+ Candidate Allocation Simulator** | *Combinatorial search, O(1) indexing*  
[Platform](https://mseat.kprsnt.in) • [Code](https://github.com/kprsnt2/mSeat)
- Built a seat-allocation simulator across 59 colleges and a 7-dimensional reservation matrix; validated within 73 ranks of the official cutoff at 90.6% dataset compression.

---

### EDUCATION
**Anurag Group of Institutions (JNTUH)** — *M. Pharmacy (Pharmaceutical Analysis & Quality Assurance)* | May 2012
