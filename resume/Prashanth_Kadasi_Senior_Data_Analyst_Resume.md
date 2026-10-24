# PRASHANTH KUMAR KADASI
**Data Analyst | ETL Pipelines, BigQuery Warehousing & BI Dashboards**  
Hyderabad, Telangana, India • +91-9948311964 • kprsnt@live.com  
Portfolio: [kprsnt.in](https://kprsnt.in) • GitHub: [github.com/kprsnt2](https://github.com/kprsnt2) • LinkedIn: [linkedin.com/in/prashanth-kumar-kadasi-b5281765](https://linkedin.com/in/prashanth-kumar-kadasi-b5281765)

---

### PROFESSIONAL SUMMARY
Data Analyst with 3.5+ years building and maintaining production data pipelines — multi-source ingestion, BigQuery warehousing, and Looker Studio dashboards that client marketing, sales, and analytics teams use day to day. At Black Piano I own 18 automated ETL pipelines and the data-quality logic behind them; earlier at Pi Software Solutions I built the Python pipelines and delivered 30+ analytical reports for US and UK clients. Before analytics, nine years at Optum auditing CMS enrollment transactions under federal compliance rules. I also build independent, self-directed analytics and agent projects — labelled separately below, not employer work.

---

### TECHNICAL SKILLS
- **Data & Analytics:** SQL, BigQuery, Looker Studio, ETL Pipeline Orchestration, Data Modeling, Data Quality & Validation, Scheduled Queries, Google Apps Script, Google Sheets Automation, Dashboard Design, SQLite
- **Languages & Tools:** Python (Pandas, NumPy, FastAPI), Node.js, TypeScript, Linux/Bash, Git, GitHub Actions, Docker, GCP, Cloud Run
- **AI-Augmented Analytics:** LLM-powered data enrichment (Gemini, ChatGPT), automated insight generation, MCP tooling for non-technical teams, RAG, prompt engineering
- **Governance & Ops:** Reference/lookup table management, retry & escalation logic, audit trails, reporting standardization, data pipeline maintenance

---

### PROFESSIONAL EXPERIENCE

**Black Piano** — *Data Analyst* | Remote  
**Mar 2026 – Present**
- Created end-to-end pipelines for various client dashboards — ingesting multi-source sector data into BigQuery and publishing to Looker Studio, with 18 automated ETL pipelines now running across 18 industry sectors.
- Built the pipelines and dashboards behind recurring industry reports (Black Friday, Christmas, sales) and ad-hoc dashboards for client marketing, sales, and analytics teams.
- Built a self-healing data-quality agent (Gemini) that resolves missing brand domains required for dashboard logo rendering: reference-table lookup with LLM fallback, writes back to both the dataset and the lookup table, retries 3x on failure, and escalates by email for human review only when unresolved.
- Developed a custom MCP tool enabling non-technical marketing and sales teams to generate publication-ready, data-grounded blog posts from a one-line prompt, backed by auto-exported Google Sheets pipelines.
- Engineered an automated AI insights pipeline (ChatGPT) producing market- and sector-level intelligence weekly, auto-published to a deployed client-facing website; reduced client manual analysis time.
- *Moved from Pi Software to Black Piano, which hires India-based talent for US/UK clients.*

**Pi Software Solutions (Pi - Datametrics)** — *Data Analyst* | Remote  
**Mar 2023 – Feb 2026**
- Built production Python data pipelines (internal `Pi-API` package) for automated BigQuery access, feeding 10+ client dashboards.
- Delivered 30+ analytical reports on US & UK industry trends for client stakeholders, standardizing reporting templates across engagements.
- Validated sources and reconciled discrepancies across concurrent client engagements, enforcing consistent metric definitions before data reached dashboards.

**Optum (UnitedHealth Group)** — *Enrollment Quality & Audit Representative (CMS Auditor)* | Hyderabad, India  
**Apr 2014 – Mar 2023**
- Audited federal enrollment transactions for Centers for Medicare & Medicaid Services (CMS) compliance, producing regulatory documentation, statutory compliance checks, and audit readiness.
- Executed end-to-end data validation and regulatory compliance checks across complex enrollment transactions, generating audit-ready documentation and discrepancy reports for CMS.
- Applied zero-tolerance quality gates to high-volume transaction datasets — the core verification and audit discipline I now apply to automated data and AI pipelines.
- Promoted via internal job posting (IJP) in March 2016 from Claims Associate (Apr 2014 – Feb 2016) to Enrollment Quality & Audit Representative based on audit precision and analytical rigor.

---

### SELECTED PROJECTS
*Independent, self-directed projects — not employer deliverables. Publicly deployed for demonstration; no business or customer metrics are claimed.*

**mSeat — Seat Allocation Simulator & Validation Model** | *Data Modeling, Validation, Compression*  
[Platform](https://mseat.kprsnt.in) • [Code](https://github.com/kprsnt2/mSeat)
- Modeled seat allocation across 59 colleges and a 7-dimensional reservation matrix, validating the model against official KNRUHS 2026 Phase 1 results — within 73 ranks of cutoff — while compressing the dataset 90.6% to fit a browser-side dataset.

**AI Eco — Automated Telemetry & Reporting Pipelines** | *Python, GitHub Actions, Data Observability*  
[Live](https://kprsnt.in/ecosystem)
- Built scheduled pipelines for repository telemetry, anomaly-free data pruning, and fitness scoring (83.4%) across 10 swarm agents, with 15+ tools and 5 resources — scheduled data operations behind strict quality gates.

**AgentSwarm — Research Output with Auditable Data Quality** | *Node.js, Hash-Chained Audit Ledger, Verification*  
[Live](https://agent.kprsnt.in/)
- Ran 34 runs with 35/35 ledger hash chains cryptographically intact; the ledger lives outside the agents' writable directory, so the audited cannot edit the audit.
- Enforced data-quality gates on unattended output: 0 oracle violations across 1,254 tool calls and 0 of 2 self-assessing agents overclaiming; an independent numerical audit verified 22/25 quantitative claims exact. Audit verdict is B+ / not publication-grade without that numerical audit.

**MyLocalCLI — Local-First Agentic Coding Assistant** | *Node.js, CLI, 8 providers, 42 tools, 38 skills*  
[Live portal](https://mlc.kprsnt.in) • [npm](https://www.npmjs.com/package/mylocalcli) • [GitHub](https://github.com/kprsnt2/MyLocalCLI)
- Published an open-source terminal coding agent on npm (`mylocalcli`, v4.0.2) — a Claude Code alternative built around local and free-tier models with no telemetry and no paid subscription required.
- Engineered **42 built-in tools** and **38 dynamic skills** across **8 providers** (Ollama and LM Studio local, vLLM self-hosted, OpenRouter and Groq free tiers, NVIDIA NIM, OpenAI, and any OpenAI-compatible endpoint), with **5 specialised sub-agents** (code reviewer, explorer, test generator, refactorer, doc writer).
- Dispatched parallel tool calls concurrently via `Promise.all` instead of sequential blocking, and added provider failover on rate limits, context overflow or connection drops — models are never silently swapped.

**Geetha — AI Spiritual Guide** | *JavaScript, SQLite, Gemini AI, Vercel*  
[Live](https://geetha.kprsnt.in/)
- Built a bilingual Bhagavad Gita application indexing all 700 verses, with dynamic AI blog generation on Gemini plus verse search, chapter navigation, and personalized context extraction — a structured-content product running on Vercel.

**rAsh Score — Multi-Model AI Brand-Visibility Index** | *Next.js, Turso/LibSQL, GitHub Actions, Vercel*  
[Live index](https://rashscore.live)
- Built and operate a live multi-model evaluation platform that queries **4 providers** (ChatGPT, Gemini, Claude, Groq) with standardised prompts and scores **300 tracked brands across 20 industry cohorts** on **4 independent dimensions** — recommendation, sentiment, prominence and factual accuracy.
- Automated daily pipelines via GitHub Actions writing into Turso (LibSQL), with a Next.js dashboard on Vercel; added a multi-agent debate arena and a text-to-SQL analyst chat.

---

### EDUCATION
**Anurag Group of Institutions (JNTUH)** — *M. Pharmacy (Pharmaceutical Analysis & Quality Assurance)* | May 2012  
