# PRASHANTH KUMAR KADASI
**Data Analyst → AI Safety & Evaluation Engineer** | *Verification & Audit Discipline, Model Steerability, Guardrails*  
Hyderabad, Telangana, India • +91-9948311964 • kprsnt@live.com  
[kprsnt.in](https://kprsnt.in) • [github.com/kprsnt2](https://github.com/kprsnt2) • [huggingface.co/kprsnt](https://huggingface.co/kprsnt) • [LinkedIn](https://linkedin.com/in/prashanth-kumar-kadasi-b5281765)

---

### PROFESSIONAL SUMMARY
Career transition into AI safety and evaluation, built on **9 years of paid verification work** as a CMS compliance auditor at Optum plus 3.5+ years as a Data Analyst (Black Piano, Pi Software). Since 2024 I have applied that audit discipline to autonomous AI systems through independent, self-directed projects: audit ledgers the agents cannot edit, per-turn scope guardrails, evidence gates that block unverified output, and measured honesty tests. Where I have not verified a number, I say so — my largest project carries an explicit **B+ / not publication-grade** verdict.

---

### TECHNICAL SKILLS
- **AI Safety & Evaluation:** Independent Verifier Design, Agent Evaluation Harnesses, Model Evaluation & Steerability, Bias Quantification, Multi-Model A/B Evaluation, Human-in-the-Loop Escalation
- **Guardrails & Audit:** Hash-Chained Audit Ledgers, Scope Guardrails, Budget Enforcement, Bounded Autonomy, Responsible Disclosure, CVSS Scoring, CWE Classification
- **Data Quality & Compliance (9 yrs):** Data Quality & Validation, Data Modeling, Regulatory Compliance Checks, Audit Readiness, Discrepancy Reporting
- **Engineering:** Python (PyTorch, Pandas, NumPy, FastAPI), Node.js, TypeScript, SQL, BigQuery, Looker Studio, Tableau, SQLite, FastMCP (MCP), RAG, Docker, GitHub Actions, GCP, Cloud Run, Linux/Bash, Git
- **Models:** Claude 4.x, Gemini 2.5/3.x, GPT-OSS 120B/20B, DeepSeek 4.1, Ollama, OpenRouter

---

### PROFESSIONAL EXPERIENCE

**Black Piano** — *Data Analyst* | Remote | **Mar 2026 – Present**
- Created end-to-end pipelines for client dashboards, ingestion through publication — **18 automated ETL pipelines** feeding BigQuery → Looker Studio across 18 sectors.- Produced **industry reports (Black Friday, Christmas, sales) and ad-hoc dashboards** for stakeholders.- Built a self-healing data-quality agent (Gemini) with **fail-safe guardrails**: resolves missing brand domains via reference-table lookup with LLM fallback, **retries 3x, then escalates via email for human review only when unresolved** — automation that knows when to stop.
- Developed a custom MCP tool letting non-technical marketing & sales teams generate data-grounded blog posts from one-line prompts.

**Pi Software Solutions (Pi - Datametrics)** — *Data Analyst* | Remote | **Mar 2023 – Feb 2026**
- Built production Python data pipelines (internal `Pi-API` package) for automated BigQuery access across 10+ client dashboards, staying reproducible.- Delivered **30+ analytical reports** on US & UK industry trends, traceable to source queries.
- **Move to Black Piano (honest note):** Black Piano hires India-based data talent to serve US/UK clients remotely; I moved for closer client-facing dashboard ownership, not a title change.

**Optum (UnitedHealth Group)** — *Enrollment Quality & Audit Representative (CMS Auditor)* | Hyderabad, India | **Apr 2014 – Mar 2023**
- Audited federal enrollment transactions for Centers for Medicare & Medicaid Services (CMS) compliance across **9 years** — regulatory documentation, compliance checks, and audit readiness in a zero-tolerance environment.
- Executed end-to-end data validation and compliance checks across high-volume enrollment transactions, generating audit-ready documentation and discrepancy reports for CMS.
- Applied zero-tolerance quality gates to high-volume datasets: verification against a written standard, evidence retained for every finding, no conclusion asserted beyond the record.
- Promoted via internal job posting (IJP) in **March 2016** from Claims Associate (**Apr 2014 – Feb 2016**) on audit precision — the discipline I now apply to AI systems: define the check, retain the evidence, refuse to overstate.

---

### INDEPENDENT & SELF-DIRECTED AI SAFETY PROJECTS
*Independent, self-directed project work — not employer work for Black Piano, Pi Software, or Optum. No claim of commercial scale, paying clients, or user take-up.*

**MyLocalCLI — Local-First Agentic Coding Assistant** | *Node.js, CLI, 8 providers, 42 tools, 38 skills*  
[Live portal](https://mlc.kprsnt.in) • [npm](https://www.npmjs.com/package/mylocalcli) • [GitHub](https://github.com/kprsnt2/MyLocalCLI)
- Published an open-source terminal coding agent on npm (`mylocalcli`, v4.0.2) — a Claude Code alternative built around local and free-tier models with no telemetry and no paid subscription required.
- Engineered **42 built-in tools** and **38 dynamic skills** across **8 providers** (Ollama and LM Studio local, vLLM self-hosted, OpenRouter and Groq free tiers, NVIDIA NIM, OpenAI, and any OpenAI-compatible endpoint), with **5 specialised sub-agents** (code reviewer, explorer, test generator, refactorer, doc writer).
- Dispatched parallel tool calls concurrently via `Promise.all` instead of sequential blocking, and added provider failover on rate limits, context overflow or connection drops — models are never silently swapped.

**rAsh Score — Multi-Model AI Brand-Visibility Index** | *Next.js, Turso/LibSQL, GitHub Actions, Vercel*  
[Live index](https://rashscore.live)
- Built and operate a live multi-model evaluation platform that queries **4 providers** (ChatGPT, Gemini, Claude, Groq) with standardised prompts and scores **300 tracked brands across 20 industry cohorts** on **4 independent dimensions** — recommendation, sentiment, prominence and factual accuracy.
- Automated daily pipelines via GitHub Actions writing into Turso (LibSQL), with a Next.js dashboard on Vercel; added a multi-agent debate arena and a text-to-SQL analyst chat.

**AgentSwarm — Measurable Agent Honesty & a Tamper-Resistant Audit Ledger** | *Node.js, Hash-Chained Ledger, Independent Oracle* | [Live](https://agent.kprsnt.in)
- Built an unattended research arena where an **independent oracle** checks every turn for phantom artifacts, fabricated numbers, and asserted verdicts on undecidable questions: **0 oracle violations across 1,254 tool calls**, **0 of 2 self-assessing agents overclaimed**.
- Kept the **hash-chained forensic ledger outside the agents' writable directory** so the audited cannot edit the audit: **34 runs, 35/35 hash chains intact**.
- Commissioned an independent numerical audit: **22 of 25 quantitative claims verified correct to the printed digits**, all 5 defects in markdown prose, not Python modules.
- Wrote two agent-authored cosmology manuscripts in REVTeX, attributed to swarm agents `A001_DarkMatter` / `A002_QuantumCosmos` — I built the system, not the physics: a **Zenodo preprint** (DOI 10.5281/zenodo.23232189) plus one **manuscript not submitted**.
- **The safety asset:** that manuscript's self-audit (`AUDIT_AND_KNOWN_LIMITATIONS.md`) found its DESI (w0,wa) agreement **circular** — the outputs are the DESI inputs — and its S8 result **tuned**, recommending against submission: the pipeline caught its own overclaim.
- **Honest limitation — the headline, not a footnote:** the verdict is **B+ / not publication-grade without that numerical audit**; no academic review.

**BugAgents — Scope Guardrails & an Evidence Gate for Autonomous Security Research** | *Python, Node.js, omp + agy* | [Live Site](https://bug.kprsnt.in)
- Enforced a **per-turn tool-call audit**: any out-of-scope host or offensive tool aborts it — a live run was aborted so, bounding the blast radius of an autonomous actor with real tool access.
- Built a **report promotion gate** (scope match + HEAD match + non-empty repro + evidence files exist) — the difference between a model that writes a report and one that found a bug: **8 findings**, **5 High/Critical**, **2 promoted**, **34 refusals**.
- Ran **22 hunt runs / 84 agent turns / 15,317 tool calls** across the `agy` and `omp` harnesses — budget enforcement and a full call log as safety properties.
- **2 submission-ready reports** were promoted, each with a reproducing proof of concept, pinned commit, and `file:line` citations — drafts only: **none submitted yet**. *(Vendor, asset, and vulnerability-class specifics withheld pending disclosure.)*
**BrandXY — Measuring and Steering Recommendation Bias in a 20B Model** | *PyTorch, LoRA/QLoRA, AMD MI300X* | [Weights](https://huggingface.co/kprsnt/BrandXY-gpt-oss-20b)
- Fine-tuned GPT-OSS-20B to **quantify and steer recommendation bias**, measured under multi-model A/B evaluation at **76.5% vs. 25.5% baseline** — open weights, so the measurement can be reproduced and challenged.

**Project Awakening — Long-Horizon Agent Behavior & Failure Recovery** | *Multi-Agent, FastMCP, CI/CD* | [Code](https://github.com/kprsnt2/ac_awakening)
- Ran an unprompted multi-agent ecosystem for **1,441 autonomous turns (1,553 commits)**, then sustained **100% CI/CD integrity across a 330-turn cloud API blackout with zero human intervention** — graceful degradation under prolonged tool failure, not silent corruption.
**AI Eco — Bounded Autonomy Under Enforceable Limits** | *Python, FastMCP, GitHub Actions* | [Live](https://kprsnt.in/ecosystem)
- Operate a **10-agent** autonomous swarm under hard constraints: living memory bounded (**<4,000 words**), target fitness scoring (**83.4%**), and technical-debt pruning gated at zero false positives.

---

### EDUCATION
**Anurag Group of Institutions (JNTUH)** — *M. Pharmacy (Pharmaceutical Analysis & Quality Assurance)* | May 2012
