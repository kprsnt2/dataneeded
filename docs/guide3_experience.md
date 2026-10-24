# Senior Resume — Interview Guide 3 of 6: Professional Experience

**Covers:** every bullet under Black Piano, Pi Software Solutions, and Optum — word by word.

---

## §1 — Black Piano — Data Analyst | Remote | Mar 2026 – Present

### 1.1 "Own the pipeline layer end to end"

> *"**Own the pipeline layer end to end** for client-facing analytics: **18 automated ETL pipelines** feeding BigQuery → Looker Studio dashboards across **18 industry sectors**, from source ingestion and scheduling through to the dashboard."*

**What it claims:** not that you built 18 things, but that you **own the layer** — ingestion, scheduling, warehouse, dashboard. That is a scope claim, and it is the senior framing.

**How to explain it step by step:**

1. **What comes in** — multi-source industry data for client dashboards, one pipeline shape per sector.
2. **What happens** — automated ingestion into BigQuery, scheduled refresh, transformation into a modelled layer.
3. **What comes out** — Looker Studio dashboards for client marketing and sales teams across 18 sectors.
4. **What "own" means** — when a pipeline breaks, it is yours. Nobody hands you a fixed feed.

**The point to make, and it is the one that lands:**

> *"Eighteen sectors isn't eighteen bespoke systems — it's one pipeline shape parameterised per sector. That's what makes it maintainable. **When the work repeats, the engineering is in the parameterisation, not in the eighteenth copy.**"*

**Likely follow-ups:**

| Question | Answer spine |
|---|---|
| *"How do you monitor 18 pipelines?"* | Row-count expectations, null-rate thresholds, freshness checks that fail loudly rather than publish stale data. Honest limit: *"Coverage is a function of the sectors we track, not the market."* |
| *"What breaks most often?"* | Schema drift at the source, and missing reference data. The second one is why the data-quality agent exists. |
| *"What's your orchestration?"* | BigQuery scheduled queries, Google Apps Script, GitHub Actions. **Do not name dbt or Airflow — you have not shipped with them.** |

**Where it can go wrong:** saying "18 pipelines" as if the number is the achievement. It is not — **the parameterisation is.** Lead with that.

**The honest limit:** *"Pipeline count isn't a quality metric. Eighteen pipelines nobody monitors are eighteen things that can fail quietly."*

---

### 1.2 "Designed and shipped a self-healing data-quality agent"

> *"**Designed and shipped a self-healing data-quality agent** (Gemini) that resolves missing brand domains autonomously — deterministic reference-table lookup first, LLM fallback for the long tail, write-back to both the dataset and the lookup table so resolutions persist. Bounded at **3 retries**, then **email escalation to a human**. The write-back converts a recurring model call into a one-time cost plus a free table lookup, so the system gets cheaper the longer it runs."*

**This is the flagship answer. Know it cold.** Four layers, in order:

1. **Detect** — a row needs a domain and does not have one.
2. **Deterministic lookup** — the reference table. Free, exact, handles the majority.
3. **LLM fallback (Gemini)** — only the residue the table cannot answer.
4. **Write-back** — to *both* the dataset and the lookup table, so the resolution becomes permanent institutional knowledge.
5. **Bounded retries ×3, then email escalation** — a human gets the residue, not the routine.

**Why the write-back is the design decision — say this:**

> *"The naive version fixes the row and moves on, and you pay the LLM cost again next week. Persisting the resolution turns a recurring model call into a one-time cost plus a table lookup. The agent gets cheaper the longer it runs — and it makes the second lookup deterministic, so the same brand always resolves the same way."*

**Why "self-healing" and not just "automated":**

> *"Automation runs a fixed procedure. This one changes its own future inputs — the write-back means the system's behaviour on the same input improves permanently. That's the difference."*

**Likely follow-ups:**

| Question | Answer spine |
|---|---|
| *"Why an LLM at all — why not just a table?"* | The failure is long-tail. A table only knows what someone already entered; the whole problem is brands nobody has entered. Table is the fast path, model generalises, write-back collapses unknown into known. |
| *"Why retry three times?"* | Transient failure — rate limits, timeouts, malformed responses — where a second attempt might genuinely succeed. It does not handle "this brand has no findable domain", so the loop is bounded. |
| *"Why email escalation rather than failing loudly?"* | An unhandled failure in a scheduled pipeline is invisible; nobody reads logs proactively. Email targets a human who can act. |
| *"How much time did it save?"* | **You do not have a measured figure.** See below. |

**The honest limit — volunteer this:**

> *"The gap is that I never instrumented the hit rate. I can't tell you the split between table-resolved and model-resolved, which means I can't prove the cost trend I just described — only that the mechanism implies it. I built the mechanism before the instrumentation, which is backwards, and it's the first thing I'd fix."*

**And the sharper limit, if you want to show real judgement:**

> *"The dangerous case isn't a missing domain — it's a confidently wrong one. A missing domain is visibly broken. A wrong domain renders the wrong logo and looks fine. And the write-back amplifies it, because a wrong answer persists. There's currently no verification step between 'the model answered' and 'we wrote it to the table'. That's the design gap I'd close first."*

**That paragraph is worth more than any metric you could invent.**

---

### 1.3 "Built a custom MCP tool"

> *"**Built a custom MCP tool** enabling non-technical marketing and sales teams to generate publication-ready, data-grounded content from a one-line prompt, backed by auto-exported Google Sheets pipelines. The engineering was grounding, not generation."*

**The insight to lead with:**

> *"A model writing marketing copy is easy. A model writing copy that is actually backed by our data, from a one-line prompt by a non-technical user, is a data-plumbing problem. The auto-exported Sheets pipelines exist so the model reads real numbers rather than inventing plausible ones."*

**Step by step:**

1. **Who uses it** — marketing and sales, non-technical, no prompt engineering skill.
2. **What they do** — type one line.
3. **What happens underneath** — data is auto-exported from the warehouse into Sheets, and the tool grounds generation in that data.
4. **Why MCP** — it exposes the capability through a standard interface rather than a bespoke integration.

**Likely follow-ups:**

| Question | Answer spine |
|---|---|
| *"How do you stop it inventing numbers?"* | Grounding — the model reads from the exported data rather than its parameters. **Honest limit:** this is grounding by construction, not a verification gate. If the export is wrong, the content is confidently wrong. |
| *"What is MCP?"* | Model Context Protocol — a standard way to expose tools and resources to a model, so the integration is not bespoke per client. |
| *"Did it get adopted?"* | **Do not claim adoption figures.** *"It's in use by the marketing and sales teams it was built for."* Nothing more. |

---

### 1.4 "Engineered an automated AI insights pipeline"

> *"**Engineered an automated AI insights pipeline** (ChatGPT) producing weekly market- and sector-level intelligence, auto-published to a client-facing site."*

**The point:** the value is **cadence**, not the model.

> *"It converted a recurring analyst task into a scheduled pipeline with a published output. The win is that it happens every week without anyone remembering to do it."*

**The honest limit:** *"It's a directional improvement — I can't quantify the time saved, because I didn't instrument it. That's a pattern in my earlier work and it's the thing I'd fix first now."*

**If pressed on quality control:**

> *"It's generation over structured inputs, auto-published. The honest position is that there's no independent verification gate on the output — a human could review it, but nothing forces that. On a client-facing site, that's a real gap."*

---

### 1.5 "Applied AI-assisted development to my own delivery"

> *"**Applied AI-assisted development to my own delivery** — using agent harnesses to compress routine work and shorten build cycles, with a human decision point wherever the pipeline cannot resolve an outcome."*

**This bullet is deliberate. Own it.**

> *"I use agent harnesses as development tooling — Antigravity, Claude Code, DeepSeek Harness, omp, pi, agy. It's how I shipped six projects while working full time. The part worth noting is the last clause: there's a human decision point wherever the pipeline can't resolve an outcome. I don't run these unattended and trust the output."*

**If challenged — "so you don't write the code yourself?"**

> *"I write less of it from scratch than a traditional engineer, and I'm precise about that. What I own is the design and the decisions — what the system should do, where the failure modes are, what the controls need to be, and why. The verification layers on my own projects exist precisely because I don't take model output on trust."*

**Why this is a strength for the roles you are targeting:** the job is automating decisions safely with AI. Someone who has already built verification around unreliable models is more useful than someone who writes clean code and trusts it.

---

## §2 — Pi Software Solutions — Data Analyst | Remote | Mar 2023 – Feb 2026

### 2.1 "Built production Python data pipelines (internal `Pi-API` package)"

> *"Built production **Python data pipelines** (internal `Pi-API` package) for automated BigQuery access across **10+ client dashboards** used by US and UK teams."*

**Why "internal package" matters:** it was not one-off scripts — it was a **reusable library** other people used.

> *"We had ten-plus dashboards needing the same BigQuery access pattern. Rather than write it ten times, it went into an internal package — so the access logic, the auth, the query patterns were defined once and consumed everywhere. That's the same instinct as the 18 pipelines: when the work repeats, the engineering is in the abstraction."*

**Likely follow-ups:**

| Question | Answer spine |
|---|---|
| *"What was in the package?"* | Authenticated BigQuery access, shared query patterns, consistent error handling. |
| *"Who used it?"* | Analytics teams across US and UK client engagements. |
| *"What would you do differently?"* | Version it properly and test it — it was an internal tool that grew, not a designed product. |

**Precision:** your resume says **10+ client dashboards**. The superseded figure in older material was "15+ enterprise dashboards" — **do not use it.**

### 2.2 "Delivered 30+ analytical reports… standardised reporting templates and reconciled source discrepancies"

> *"Delivered **30+ analytical reports** on US and UK industry trends; standardised reporting templates and reconciled source discrepancies across concurrent client engagements."*

**Three distinct claims — separate them:**

1. **30+ reports** — volume over three years.
2. **Standardised templates** — the same repetition-to-abstraction instinct.
3. **Reconciled source discrepancies across concurrent engagements** — this is the one that connects to your compliance background.

**The reconciliation answer:**

> *"Different sources disagreeing on the same metric was routine. You assume the difference is real and find it rather than assuming one side is wrong: first check whether the metric definitions actually match, because the same name often means different filters or different date logic. Then trace both to source and check the join — an inner join silently drops unmatched rows, and that's the most common cause. Then time zone and cutoff boundaries. Then duplicates inflating one side. And you resolve it by picking one definition, documenting it, and making both reports read from the same governed query — because reconciling the numbers without fixing the definition means it recurs next month."*

---

## §3 — Optum (UnitedHealth Group) — Apr 2014 – Mar 2023

### 3.1 "Audited federal enrollment transactions for CMS compliance"

> *"Audited federal enrollment transactions for **Centers for Medicare & Medicaid Services (CMS)** compliance, producing regulatory documentation, statutory compliance checks and audit-ready discrepancy reports."*

**Be precise about the domain — this is the single most important precision on the resume.**

It was **enrollment** — the application and eligibility stage where a member's coverage is established. **Not claims adjudication.**

> *"To be clear about what it was: enrollment transactions — the application and eligibility stage, governed by CMS rules. Not claims adjudication. I'd rather say that plainly than let it sound broader than it was."*

**What it gives you that transfers:**

- **Regulatory documentation** — producing records that stand up to an external auditor.
- **Statutory compliance checks** — applying a written rule set to a high-volume stream of transactions.
- **Audit-ready discrepancy reports** — finding and documenting exceptions, not just processing the happy path.

**The bridge line:**

> *"Every decision had to be traceable to a rule and defensible to an auditor. That's the same requirement these job descriptions put on automated decisions — explainable, auditable, aligned with regulatory requirements."*

### 3.2 "Applied zero-tolerance quality gates to high-volume transaction datasets"

> *"Applied **zero-tolerance quality gates** to high-volume transaction datasets — every decision traceable to a rule and defensible to an external auditor. This is the discipline I now build into automated systems."*

**"Zero-tolerance" means:** a transaction that failed a rule did not pass with a warning. It failed.

**Why this is the strongest bridge in your resume:**

> *"Zero-tolerance means the gate either passes or it doesn't — there's no 'needs review' label that lets something through. I build the same way now. In BugAgents the promotion gate has four conditions and a candidate that fails any one doesn't get a warning label — it doesn't promote. And in JobAgents, generated text that fails validation is never written to disk."*

**The line worth memorising:**

> *"If the rule isn't enforced by something that can reject the output, it isn't a rule — it's a suggestion."*

### 3.3 "Promoted in Mar 2016 from Claims Associate on audit precision and analytical rigour"

> *"Promoted in Mar 2016 from Claims Associate on audit precision and analytical rigour."*

**This line does two jobs, and you should use both:**

1. **It evidences progression** — you were promoted on performance, not tenure.
2. **It records that you started as a Claims Associate** — a genuine claims-function title at a US health payer, relevant if the role is in insurance or healthcare.

**If the role involves claims, say it early:**

> *"I started at Optum as a Claims Associate, then moved into enrollment quality and audit for the rest of my nine years. So I've been on the claims side of a health payer — though I want to be straight: that was US Medicare and Medicaid, and it's a long way back in role terms. I'm not going to pretend it makes me a claims operator today."*

**Be ready for "what did you actually do as a Claims Associate?"** If you can describe it concretely, it is a strong card. **If you cannot, mention it once and move on** — do not lean on it.

---

## §4 — Practice set for this guide

| # | Question |
|---|---|
| 1 | Walk me through the 18 pipelines. What does "own end to end" mean? |
| 2 | Tell me about the self-healing agent — why is it self-healing? |
| 3 | How much time did the agent save? *(No figure — give the mechanism and the gap.)* |
| 4 | What's the dangerous failure mode of that agent? |
| 5 | What is MCP and why did you use it? |
| 6 | You used AI to build these. Isn't that a problem? |
| 7 | What did the `Pi-API` package actually do? |
| 8 | Two reports disagree. How do you resolve it? |
| 9 | You audited enrollment — is that claims experience? |
| 10 | What does "zero-tolerance quality gate" mean in practice? |

---

*← Guide 2: Profile & Capabilities · Guide 4: Selected Systems →*
