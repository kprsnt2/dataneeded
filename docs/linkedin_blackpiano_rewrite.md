# LinkedIn Rewrite — Black Piano, Framed for Data Pipelines & Automation

**Why this rewrite:** ICICI Lombard's recruiter named **"data pipelines"** and **"automated pipelines"** in his first message. Your current LinkedIn section leads with the data-quality agent and mentions the 18 pipelines last. For this inbound — and for any data-engineering-flavoured req — the pipeline and automation work should lead, because that is the keyword he is searching on.

**What this rewrite does and does not do:**
- ✅ Reorders and sharpens what you already have, using only phrases from [../config/profile.md](../config/profile.md).
- ✅ Keeps the title **Data Analyst**. No inflation, no "Engineer" title.
- ⛔ Does not invent a metric. Every number below is either already in the canonical profile, or flagged in §1–§2 as a template value being removed.

> **Evidence of current state:** [assets/linkedin_blackpiano_current.png](assets/linkedin_blackpiano_current.png)

---

## §1 — RESOLVED: the 60% claim comes off

**Decision taken (2026-10-12): remove it.** You confirmed it was left on LinkedIn by mistake. That was the right call, and here is why it mattered:

| Claim on your live profile | In `config/profile.md`? | In `config/profile.example.md`? |
|---|---|---|
| "reduced client manual analysis time by **60%**" | ❌ **No** — the canonical file deliberately drops the figure | ✅ Yes, line 42 |
| "...across 18 sectors for **4 enterprise clients**" | ❌ **No** — canonical says only "across 18 industry sectors" | ✅ Yes, line 43 |

`profile.example.md` is the **template** file. The example's phrasing had been copied into LinkedIn, and the canonical file was later tightened to remove the 60% — but LinkedIn was never updated. **Your live profile was claiming a number your own prep doc explicitly told you not to say aloud.** In a recorded, transcript-scored interview that is a trap, not a rounding error.

**The standing rule, so this cannot recur:** if a number is not in `config/profile.md`'s Verified Metrics table, it does not go on LinkedIn, in a resume, or in an interview answer. `profile.example.md` is a template — **never a source.**

**On "4 enterprise clients":** you said approximate, so it becomes **"multiple enterprise clients"** below. That still conveys multi-client scope without asserting a count you'd have to defend.

---

## §2 — The same defect is probably one section further down: your Pi Software entry

**The Black Piano bullets were not the only thing copied from the template.** `config/profile.example.md` differs from the canonical profile in two more places — and if the Black Piano bullets leaked into your live LinkedIn, these plausibly did too:

| `profile.example.md` (template) | `config/profile.md` (canonical) | Risk |
|---|---|---|
| Line 37: title **"Data Analyst / AI Systems"** | Line 34: *"The title is **Data Analyst** at both employers — **do not inflate it**."* | "AI Systems" appended to a held title is the exact inflation the canonical file forbids. |
| Line 48: **"15+ enterprise dashboards"** | Line 96: **"Client dashboards (Pi), 10+"** | A stale count, **and** "enterprise dashboards" is explicitly listed in [`outreach_templates.md` §6](outreach_templates.md) as superseded wording. |

**Your screenshot only showed the Black Piano section, so I cannot see your Pi Software entry or your title line.** Check both now:

1. **Your profile headline and the Pi Software job title.** If either says **"Data Analyst / AI Systems"**, change it to **"Data Analyst"**. Keep the *direction* in your headline if you want it (that is allowed — see §5), but not on a held job title.
2. **The Pi Software bullet that mentions dashboards.** If it says **"15+ enterprise dashboards"**, change it to **"10+ client dashboards"** — the verified figure. Search your profile for the strings `15+`, `enterprise dashboards`, and `AI Systems`.
3. **While you are there, read the whole profile once logged out.** This defect class — a template value surviving into a live profile — has now produced three separate problems: the 60%, the client count, and possibly the title. A single logged-out read catches all of them.

**Why this matters more than it looks:** the 60% sat on your live profile unnoticed. That means the profile has not been read critically since it was written. Anything on it that is not in the canonical profile is a question you will one day be asked and cannot answer.

---

## §3 — Proposed Black Piano section (publish this)

Copy the bullets as-is. This is the recommended version, with both corrections applied.

```
Data Analyst
Black Piano · Full-time
Mar 2026 - Present · Hyderabad, Telangana, India · Remote

• Architected 18 automated ETL pipelines feeding BigQuery → Looker Studio
  dashboards across 18 sectors for multiple enterprise clients — owning the
  pipeline layer end to end, from source ingestion and scheduling through to the
  client-facing dashboard.

• Built a self-healing data-quality agent powered by Gemini: autonomously
  resolves missing brand domains via reference-table lookup with LLM fallback,
  writes results back to both the dataset and the lookup table, retries 3x, and
  escalates by email for human review only when unresolved.

• Engineered an automated AI insights pipeline (ChatGPT) generating market- and
  sector-level intelligence weekly, auto-published to a deployed client-facing
  website, reducing a recurring manual analysis step.

• Developed a custom MCP (Model Context Protocol) tool enabling non-technical
  marketing & sales teams to generate publication-ready, data-grounded blog
  posts from a one-line prompt, backed by auto-exported Google Sheets pipelines.

• Worked on recurring industry reports (Black Friday, Christmas, sales) and
  ad-hoc dashboards, automating the refresh where the cadence allowed.
```

### Why these bullets, in this order

| Bullet | The signal it sends |
|---|---|
| **1. The 18 pipelines** | *Volume and ownership.* "18 pipelines across 18 sectors" is the single strongest data-engineering line you have, and it is the exact phrase the recruiter used. Moving it to the top is the whole point of this rewrite. |
| **2. The data-quality agent** | *Automation with judgement.* This is the differentiator — most analysts don't build self-healing systems. Kept second because it's your best story, not your broadest. |
| **3. The AI insights pipeline** | *Cadence and client impact.* "Weekly, auto-published" says scheduled production, not a one-off analysis. |
| **4. The MCP tool** | *Stakeholder leverage.* Non-technical users, one-line prompt, grounded in real data. This is the bullet a hiring manager remembers. |
| **5. Recurring reporting** | *The unglamorous proof.* Recurring reports are exactly what an insurer's MIS team needs and rarely gets — and this bullet is deliberately worded as *"automating the refresh where the cadence allowed"* rather than claiming full automation, because I can't confirm those reports are genuinely scheduled. Upgrade it only if they are. |

**The added clause in bullet 1 — "owning the pipeline layer end to end, from source ingestion and scheduling through to the client-facing dashboard"** — is not a new claim. It restates what you already say across the six canonical bullets (pipelines, scheduling, dashboards), and it is the phrase that answers the question the recruiter is actually asking: *does this person own the pipeline, or just query it?* You own it.

**Bullet 5 is a reframe, not an addition** — and I have deliberately kept the canonical verb ("Worked on") rather than upgrading it to "Automated", because I do not know whether those reports are genuinely scheduled or were produced manually each cycle. **If they are scheduled and recurring, change it to "Automated recurring industry reporting…" — that is a stronger and equally honest bullet.** If they are produced by hand, leave it as written. Only you can settle this, and it is the kind of claim an interviewer probes with one follow-up question.

**Bullet 3 uses "reducing a recurring manual analysis step", not "replacing".** Your canonical profile says *"reduced client manual analysis time"* — it does not claim the step was eliminated. "Reducing" is the defensible verb; "replacing" asserts more than you can support, and it is exactly the upgrade the data-quality-agent guidance elsewhere in your prep warns against.

**What changed from your live version:** the 60% is gone (replaced with *"reducing a recurring manual analysis step"* — true, and unfalsifiable in the good sense); "4 enterprise clients" is now "multiple enterprise clients"; and the pipeline bullet moved from last to first.

---

## §4 — Headline and About: make the keyword land

Your section is only half the surface. The recruiter is searching on keywords, so the pipeline language needs to appear above the fold too.

### Headline — pick one

```
Data Analyst → Data Pipelines & Automation | Python · SQL · BigQuery · GCP
```
```
Data Analyst | 18 Automated ETL Pipelines → BigQuery · Looker Studio | Python, SQL, GCP
```
```
Data Analyst · Data Pipelines, Data Quality & Automation | Python · BigQuery · GCP · SQL
```

**Why `→` and not `|`:** `Data Analyst → Data Pipelines & Automation` describes a direction without asserting a title you don't hold. It is honest, and it is the same convention your resumes already use.

**Do not use:** "Data Engineer", "Senior", "Lead", "Analytics Engineer" as a held title. Your title is Data Analyst at both employers, and the profile rule against inflating it is binding.

**A note on where the strict skill rule applies.** Your headline and About are prose — "data pipelines" and "automation" are descriptions of the work, and describing your work accurately is not a skill claim. **The strict rule bites on the Skills section (§5)**, where every entry should be traceable to the canonical list. Keep that boundary in mind: describe freely in prose, list conservatively in Skills.

### About section — draft

```
I build the data pipelines behind client dashboards — and the quality gates
that decide whether what lands in them can be trusted.

Currently at Black Piano, where I architected 18 automated ETL pipelines feeding
BigQuery → Looker Studio dashboards across 18 sectors for multiple enterprise
clients. Before that, three years at Pi Software Solutions building production
Python pipelines for automated BigQuery access across 10+ client dashboards and
delivering 30+ analytical reports for US and UK clients.

The work I care most about is automation with a boundary. I built a self-healing
data-quality agent that resolves missing data autonomously — deterministic
lookup first, an LLM for the long tail, write-back so the fix persists — and
escalates to a human only when it genuinely cannot resolve something. Before
data, I spent nine years auditing CMS enrollment transactions at Optum, which is
where I learned to treat data quality as a gate rather than a report.

I also build autonomous agent systems on my own time — a job-sourcing pipeline,
a research arena, a pair of security-research agents. Those are independent
projects, not client work.

Python · SQL · BigQuery · GCP · Looker Studio · ETL orchestration · data
modelling · data quality & validation

kprsnt.in · github.com/kprsnt2
```

**Note what the About does:** it leads with pipelines (the recruiter's keyword), states the automation work second, uses the Optum audit background as the credibility spine rather than an awkward pre-2023 chapter, and explicitly labels the independent projects as independent — which is the attribution rule your own pipeline enforces in code.

---

## §5 — Skills to list

Your screenshot shows the first two skills as **"Python (Programming Language)"** and **"Data Engineering"**, then "+6 skills".

**"Data Engineering" is not in your verified skills list.** That does not make it a lie — it is a reasonable description of what you do — but it is a title-adjacent claim on a profile whose canonical rule is that your held title is Data Analyst, and it invites the question *"so are you a data engineer?"* which you then have to walk back.

**Two options, both fine:**
- **Keep it** — and be ready to answer plainly: *"My title is Data Analyst. The work has been data engineering — pipelines, orchestration, warehouse modelling — and I describe it that way rather than claiming the title."* That is a good answer and it costs you nothing.
- **Replace it with a verified skill that carries the same signal.** The canonical list has exactly the right ones: **`ETL Orchestration`**, **`Data Pipeline Maintenance`**, or **`Data Modeling`**. All three are in [../config/profile.md](../config/profile.md), all three are unambiguously true, and they carry no title implication.

**My recommendation: replace it with `ETL Orchestration`.** You keep the pipeline signal, lose the ambiguity, and stay strictly inside the verified skill list.

**Note the rule I am applying to myself here:** I originally suggested replacing it with "Data Pipelines" — which is *not* in the canonical Skills list either. That would have swapped one unverified skill for another. The canonical list has the phrase you need; use its exact wording.

LinkedIn allows up to 50 skills, and the first three are the ones that matter for search.

**Pin these three first** — all three are verbatim in the canonical Skills list:
1. **ETL Orchestration**
2. **Python** (LinkedIn will render it as "Python (Programming Language)")
3. **SQL**

**Then, verbatim from the canonical Skills list** (with one LinkedIn-rendering note below):

`BigQuery` · `Looker Studio` · `Tableau` · `ETL Orchestration` · `Data Modeling` · `Data Quality & Validation` · `Data Pipeline Maintenance` · `Scheduled Queries` · `Google Apps Script` · `SQLite` · `Google Cloud Platform (GCP)` · `Cloud Run` · `Docker` · `GitHub Actions` · `Vercel` · `Linux/Bash` · `Git` · `Python` · `Pandas` · `NumPy` · `FastAPI` · `Node.js` · `TypeScript` · `JavaScript` · `Multi-Agent Swarms` · `FastMCP (MCP)` · `Tool/Function Calling` · `RAG` · `Prompt Engineering` · `LoRA/QLoRA Fine-Tuning` · `Agent Evaluation Harnesses` · `Human-in-the-Loop Escalation` · `Bounded Autonomy`

**Four labels I had wrong in the previous version of this list — corrected, because the rule applies to me too:**

| I had written | Canonical is | Why it matters |
|---|---|---|
| `Data Quality` **and** `Data Validation` | **`Data Quality & Validation`** (one entry) | The canonical list has it as a single combined skill. Listing two implies a granularity you can't support. |
| `Data Analysis` | **`Data Pipeline Maintenance`** | `Data Analysis` is not in the Skills list at all. `Data Pipeline Maintenance` is, and it is closer to the work you actually do. |
| `Multi-Agent Systems` | **`Multi-Agent Swarms`** | The canonical term. "Systems" is a softer word than the thing you actually built. |
| `Large Language Models (LLM)` · `Fine-Tuning` · `Agent Evaluation` | Fine as category headings — but the canonical forms are **`LoRA/QLoRA Fine-Tuning`** and **`Agent Evaluation Harnesses`** | Use the canonical form where you have room. |

**LinkedIn rendering note:** LinkedIn's own skill taxonomy will map some of these to its canonical names — `Python` becomes "Python (Programming Language)", `GCP` becomes "Google Cloud Platform (GCP)". Accept LinkedIn's mapping where it offers one; the point is that every entry traces to your Skills list, not to a word you liked.

**Do not add:** `dbt`, `Airflow`, `Spark`, `Snowflake`, `Databricks`, `AWS`, `Azure`, `Power BI`, `Excel` (advanced), `VBA`, `Data Engineering`. None are in your verified skills, and adding any of them creates the exact gap an interviewer finds in the first five minutes.

---

## §6 — How this connects to the ICICI conversation

Publishing **§3** makes your profile and your interview script agree, and three things improve at once:

1. **The recruiter's keyword is above the fold.** "Data pipelines" and "automated" now appear in your headline, your first bullet, and your About. He found you by searching for that language.
2. **The 60% contradiction is gone.** Until you edit, your live profile claims a number your prep doc explicitly tells you not to say. In a recorded, transcript-scored interview that is a live trap — and it is the kind of thing an interviewer who read your profile will ask about directly.
3. **You can answer "what do you own?" with one line.** *"Eighteen automated ETL pipelines into BigQuery feeding Looker Studio dashboards across eighteen sectors — I own the pipeline layer, from ingestion and scheduling through to the dashboard."*

**The line to say in the interview, unchanged by any of this:**

> *"The interesting engineering was never getting a model to produce output — it was building the component that decides whether to believe the output."*

---

## §7 — Publish checklist

- [x] Decide the 60% question — **resolved: remove it** (§1)
- [x] Confirm or soften "4 enterprise clients" — **resolved: "multiple enterprise clients"**
- [ ] Update the **headline** (§4)
- [ ] Update the **About** (§4)
- [ ] Replace the **Black Piano bullets** with §3
- [ ] **Check the Pi Software entry and your job title** for `15+`, `enterprise dashboards`, `AI Systems` (§2)
- [ ] Pin **ETL Orchestration / Python / SQL** as the top three skills (§5)
- [ ] Do **not** add any tool from the "Do not add" list
- [ ] **After publishing, open the profile in a logged-out browser and read it once.** The 60% survived on the live profile for months precisely because it was never re-read. Thirty seconds now saves an interview later.

---

*Companion files: [icici_lombard_interview_prep.md](icici_lombard_interview_prep.md) · [micro1_data_analyst_prep.md](micro1_data_analyst_prep.md) · [micro1_ai_agent_evaluator_prep.md](micro1_ai_agent_evaluator_prep.md) · [outreach_templates.md](outreach_templates.md) · [../config/profile.md](../config/profile.md)*
