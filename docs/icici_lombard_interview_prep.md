# ICICI Lombard — Inbound Interview Prep

**Trigger:** LinkedIn DM from **Swarnim Vaidya — "Leadership Hiring | ICICI Lombard"**, 2026-10-12.
**Candidate reply already sent:** *"Hi Swarnim, thank you for reaching out. I would like to learn more about this opportunity."*
**Ground truth for every number in this file:** `config/profile.md` (reconciled 2026-10-11). If a figure is not in that file, it does not get said out loud.

---

## §0 — The 60-second read

1. **He has not told you what the job is.** No title, no level, no location, no JD, no comp. Everything below is contingent on that. The single highest-value action is to get the JD before preparing further — §1.
2. **What he actually responded to:** your LinkedIn *work*, not your resume. He named the **data-quality agent** and **automated pipelines** specifically. That means your **Black Piano** work is the door he opened — lead with it, not with the independent projects.
3. **The best project to explain in detail is the self-healing data-quality agent.** It is the only project in your portfolio that is simultaneously: (a) **employer work**, (b) **Python + data analytics**, (c) **autonomous AI**, and (d) **exactly what he quoted back at you**. Full walkthrough: §4.
4. **Four risks to price in early — all sourced below and in [icici_lombard_research.md](icici_lombard_research.md):**
   - **Recruiter identity is unverified.** Nothing found confirms Swarnim Vaidya works at ICICI Lombard. Verify before you send documents — §1.3.
   - **Stack mismatch.** Verified evidence points to **AWS and Microsoft Azure**. There is **no evidence of GCP, BigQuery, or Looker** at the company — your core platform. See §2.5.
   - **Location.** ICICI Lombard is Mumbai-headquartered; you are Hyderabad-based and remote-first. Likely the hard blocker. See §2.6.
   - **Seniority banding.** ~3.5 years in data against 12.5 years total. Insurers price analytics on years-in-data. See §2.4.
5. **Where you are strong for an insurer specifically:** nine years at Optum auditing CMS enrollment transactions under a federal regulator. General insurance is a regulated, audit-heavy, reconciliation-heavy business. That is a genuine, non-obvious advantage — and it is not a keyword anyone else in the pile has.
6. **The good news, verified:** the AI framing in his message is **not invented**. ICICI Lombard has an AI health-underwriting engine, multilingual Voice AI (reported as >1M customer conversations handled), an AI travel planner, a digital insurance branch, and a CTO who has spoken publicly about AI since 2021 — and about AI-driven fraud detection since at least 2024. The company is genuinely digitising — this is not an AI-washing employer.

> **Research brief:** [icici_lombard_research.md](icici_lombard_research.md) — every claim tagged VERIFIED / WEAK / UNVERIFIED, with the blocked-source log. Read §D and §E of that file before the screening call.

---

## §1 — What he wants (and how to find out)

### 1.1 Read the message for what it is

| He wrote | What it actually is |
|---|---|
| "I came across your profile and was impressed by your work at Black Piano" | Template personalisation. Real signal: he read your profile, or a tool summarised it. |
| "Your experience in building autonomous AI systems and data pipelines" | The two things he is sourcing for. Note: **both are things you do at an employer**, which is why he led there. |
| "Python and data analytics" | The requirement keywords. Broad enough to cover Data Analyst → Data Engineer → Data Scientist. |
| "You've done an amazing job with your data-quality agent and automated pipelines" | Specific, and it matches your Black Piano bullets. This is the hook to lean into. |
| "I noticed you're open to new opportunities" | LinkedIn's `#OpenToWork`-style signal. This is why he messaged *you* — not a deep evaluation. |
| "Leadership Hiring" | **Ambiguous and load-bearing.** In Indian insurers this usually means "hiring for senior/lead roles", not "I am a leader". It could also be a team name. Ask (§1.5, Q2). |
| No JD, no title, no level, no comp | Standard for first-touch. Not a red flag by itself — but it means you cannot prepare specifically until you ask. |

**Honest read:** this is a **volume-sourced first touch from a recruiter with a real req behind it**, personalised with profile detail. The compliment is not evidence of a role fit. The *specificity* of "data-quality agent" is evidence he (or his tooling) actually looked — which is mildly better than a pure blast.

### 1.2 The three things this role most likely is

Ranked by fit against what he named:

| Rank | Likely role family | Why | Your fit |
|---|---|---|---|
| 1 | **Analytics / Data Engineer** (Python pipelines + warehouse + BI) | "data pipelines", "Python", "automated pipelines" | **Strong.** 18 ETL pipelines → BigQuery → Looker Studio at Black Piano; production Python `Pi-API` package at Pi Software. |
| 2 | **Data Analyst (senior/lead)** | "data analytics", "data-quality agent" | **Strong on work, wrong on title.** Your title is Data Analyst at both employers — which is honest and also *fine* for an analyst req. |
| 3 | **Data Scientist / AI-ML analyst** | "autonomous AI systems" | **Partial.** You build agentic systems and fine-tune (BrandXY), but you have no classical ML/statistics-modelling employment history. Do not oversell this one. |

Low-probability but possible: an **MIS/BI reporting** role (Power BI/Tableau + SQL, less Python) — in which case your BigQuery/Looker work still maps, but the autonomy story is a bonus rather than the point.

**A caution on the ranking.** The recruiter's *language* is broad, and his *stated* interests ("Python and data analytics") sit closest to ranks 1–2. But note what is **not** in the message: no mention of cloud, warehouse, BI tooling, or agent frameworks. That is consistent with a recruiter working from a keyword list rather than a detailed JD — which is another reason to get the JD before preparing further.

### 1.3 Before you send anything: verify the recruiter

**The finding:** no source reachable in this session confirms that **Swarnim Vaidya** works at ICICI Lombard. LinkedIn profiles and job pages require authentication, so this is an **unverified** gap, not a proven problem — but it is a gap, and it matters because the next step in a normal recruiter process is a request for documents.

**This is not an accusation.** Plenty of legitimate recruiters are third-party, RPO, or agency-side and simply describe themselves by the client they are hiring for. But "no JD, no title, no level, no comp, unverified identity" is also the exact profile of a harvesting approach, so verify cheaply before sharing anything.

**Do this — it takes five minutes:**

1. **Open his LinkedIn profile.** Does the *Experience* section list ICICI Lombard, and for how long? A recruiter describing himself by client name usually has an agency or RPO employer in that field. Either answer is fine — you just want to know which.
2. **Check mutual connections and activity.** Does he post or comment? A real recruiter in a real req usually has a visible footprint.
3. **Ask the two questions that a genuine recruiter answers instantly:** *"Are you on ICICI Lombard's own payroll or a partner/RPO?"* and *"Can you share the JD or a requisition ID?"* A funded req has a JD. A harvest cannot produce one.
4. **Never send, before a JD exists:** PAN, Aadhaar, bank details, a scanned ID, your date of birth, or a signed offer or NDA. A legitimate Indian recruitment process does not need identity documents at first-contact stage. If documents are requested before a JD, that is your answer.
5. **Verify the email domain if he moves you to email.** A message from a personal Gmail claiming to represent an insurer is not disqualifying by itself, but it is worth noting.

**If it is a third-party recruiter,** the role may still be real — but ask who the **employer of record** is. Agency-placed roles at insurers often carry different bands, benefits, and conversion prospects from direct payroll, and you want to know which one you are in before investing rounds.

### 1.4 The message to send next — copy-paste ready

You have already sent the polite opener. **Do not send another pleasantry.** Send one message that (a) asks for the facts you need, (b) proves fit in one line, (c) offers a call. Short, specific, easy to answer.

**LinkedIn DM (recommended, ~850 characters):**

```
Hi Swarnim, thanks for the follow-up. Before we spend each other's time, could
you share four things:

1. The job title and level (IC vs. people-manager)
2. Location and work model — Mumbai on-site, hybrid, or remote
3. The team it sits in — analytics, data engineering, or the AI/digital side
4. The JD or a link to the posting

Quick context so you know what you'd be getting: I'm a Data Analyst with 3.5+
years in production data work. At Black Piano I own 18 automated ETL pipelines
feeding BigQuery and Looker Studio across 18 industry sectors, plus the
self-healing data-quality agent you mentioned. Before that, 9 years at Optum
auditing CMS enrollment data under a federal regulator.

Happy to jump on a 15-minute call this week — my portfolio is https://kprsnt.in
```

**Why this shape:** it asks four answerable questions in priority order — location second, because it is the most likely blocker (§2.6) — gives him a reason to reply fast, and the proof block is the same verified set you use everywhere. **Do not** quote comp in this message — §2.4.

**Email version** if he moves you off LinkedIn — subject: `Re: ICICI Lombard opportunity — quick questions before a call`, same body, sign with `kprsnt@live.com · +91-9948311964 · https://kprsnt.in`.

### 1.5 The 12 questions to ask on the screening call

Ask the first five even if the call is 15 minutes. The rest are for when it goes well.

| # | Question | Why it matters to you |
|---|---|---|
| 1 | "What's the exact title and level — is it an individual contributor role or does it carry a team?" | Your titles are Data Analyst. If it's a manager req, you are not the candidate and should not pretend otherwise. |
| 2 | "Which team does it sit in, and who does it report to?" | Analytics vs data engineering vs AI/digital are three different jobs with the same keywords. |
| 3 | "Where is it based, and is remote or hybrid possible?" | You are remote-first. This is a gating fact, not a preference. |
| 4 | "What's the budgeted range for the band?" | Ask early — see §2.4. Indian insurer bands and your remote/USD expectation may simply not overlap. |
| 5 | "What does success look like in the first six months?" | The single best predictor of whether the role is real and scoped. Vague answer = not yet scoped. |
| 6 | "Is this a replacement or a new headcount, and why now?" | New headcount with a reason is a better bet than backfill churn. |
| 7 | "What does the data stack look like today — warehouse, orchestration, BI tool?" | Determines whether BigQuery/Looker transfers or you'd be learning Oracle/SQL Server + Power BI. |
| 8 | "Is the team on-prem or cloud, and is there a migration underway?" | Same reason. Ask it as curiosity, not as a demand. |
| 9 | "How much of the work is reporting/MIS versus building pipelines and automation?" | You want the build side. Some "analyst" reqs are 90% recurring reports. |
| 10 | "Who makes the hiring decision, and what are the next two steps after this call?" | Separates a real req from a pipeline-building exercise. |
| 11 | "Is there an internal candidate already in the process?" | Polite, and the answer is often revealing. |
| 12 | "What's the timeline — when would you want someone to start?" | A live req has a date attached. |

**Signal to watch:** if he cannot answer #1, #2 or #7, this is likely early-stage sourcing rather than a defined role. That is not fatal — but it changes it from "interview prep" to "stay warm and let him come back with the JD."

---

## §2 — Fit, gaps, and the honest risk list

### 2.1 What you bring that the req named

| He asked for | Your verified evidence (source: `config/profile.md`) |
|---|---|
| Python | Production Python pipelines via the internal `Pi-API` package for automated BigQuery access across 10+ client dashboards (Pi Software). Python is also the language of JobAgents, BugAgents and the AI Eco stack. |
| Data analytics | 18 automated ETL pipelines → BigQuery → Looker Studio across 18 industry sectors; 30+ analytical reports for US & UK industry trends (Pi Software); industry reports (Black Friday, Christmas, sales) and ad-hoc dashboards at Black Piano. |
| Data pipelines | The 18 ETL pipelines above; the auto-exported Google Sheets pipelines behind the MCP blog tool; scheduled queries and BigQuery Notebook in the verified skills list. |
| Data quality | **The self-healing data-quality agent** — the exact thing he quoted. Plus the whole JobAgents anti-fabrication guard (catches 8/8 seeded fabrications). |
| Autonomous AI systems | JobAgents, AgentSwarm, BugAgents, AI Eco — all independent, all live, all verifiable. Label them as **your own projects, not employer work** (see §2.3). |

### 2.2 The gaps — say these before he finds them

Volunteering a limitation is the fastest credibility you can buy. Have these ready, unhedged:

1. **No general-insurance domain experience.** Your regulated-domain experience is **US healthcare** (CMS/Medicare enrollment audit at Optum), not **IRDAI/general insurance**. Say it plainly, then bridge: *"Different regulator, same discipline — reconciliation, audit trail, and being able to defend a number to an auditor."*
2. **No classical ML / statistical modelling in employment.** Your ML work is fine-tuning and evaluation (BrandXY: GPT-OSS-20B, 76.5% vs 25.5% baseline), not forecasting, GLMs, or pricing models. If the req is a data-science req, this is a real gap.
3. **No people management, ever.** 3.5 years of IC data work plus 9 years of audit. If "Leadership Hiring" means a manager req, that is disqualifying and you should find out fast.
4. **Titles are Data Analyst at both employers.** Not "Senior", not "Lead", not "Engineer". Do not inflate — the moment you do, every other claim becomes suspect.
5. **No dbt, no Airflow, no Spark, no Snowflake/Databricks in the verified skills list.** If the JD names them, say *"I've built orchestration and scheduling without those specific tools — BigQuery scheduled queries, Google Apps Script, GitHub Actions. I'd expect to pick up dbt or Airflow quickly; I haven't shipped with them."*

### 2.3 The positioning rule that matters most here

**Black Piano and Pi Software are employers. JobAgents, AgentSwarm, BugAgents, AI Eco, BrandXY, mSeat and Awakening are your own projects.** Your own pipeline's validator rejected a model output that merged them — that's how real the trap is.

Correct framing, every time:

> *"At Black Piano I build the client-facing data work — the pipelines, the dashboards, the data-quality agent. Separately, on my own time, I build autonomous agent systems: a job-sourcing pipeline, a research arena, a security-research pair. Those are independent projects, not client work."*

That sentence does two jobs: it is honest, and it signals that you build things nobody asked you to build — which is exactly the trait a "Python + automation" req is fishing for.

### 2.4 Comp — resolve this before you invest hours

**The likely mismatch.** Your own recorded position is **remote-first** (profile: *"India (Hyderabad base) + Remote-global"*). **If your package is USD-linked, say so — the mismatch argument is strongest in that case. If it is INR-denominated, then the gap is about the band, not the currency.** *(No dollar figure is quoted here on purpose: it is not in [../config/profile.md](../config/profile.md), so confirm your own walk-away number before you use it as a line. An unsourced figure in a prep doc becomes a figure said aloud.)* An India-based general insurer hiring a Data Analyst / Analytics Engineer will typically band well below a remote-global baseline in INR terms, even at a senior IC level. These two positions may simply not overlap.

**How to handle it without anchoring low:**

1. **Ask for their range first** — this is already your stated preference and it is the right one here. Question #4 in §1.5.
2. If pushed for your number early, redirect once: *"I'd rather understand the scope first — a lead analytics role and a reporting role aren't the same job. What band is budgeted for this?"*
3. If they insist, give a range anchored to **scope**, not to your history: senior IC analytics/engineering in India with Python + cloud warehouse experience. Do not quote the USD figure at an India-based insurer unless the role is genuinely remote-global with a USD-denominated contract.
4. **Watch for the tell:** if the recruiter deflects the budget question twice, the band is probably below your floor. That is useful information, cheaply obtained.

**Do not** spend three interview rounds discovering a 60% gap. Ask in the screening call.

**The banding trap — the part that is easy to miss.** You have **~12.5 years of total work experience but only ~3.5 years in data** (2023–present; the prior nine were CMS auditing). Indian insurers price analytics roles largely on **years-in-data**. So you can be screened *into a band that underprices your total seniority* while simultaneously reading as *too senior in years for an entry IC role*. That mismatch — not the currency — is the most likely source of a disappointing number, and it is worth naming on the call rather than discovering in an offer:

> *"One thing worth flagging early: my nine years before this were in regulated data auditing at Optum, and the last three and a half have been building pipelines and data-quality systems. So I'd rather you price the scope of the role than count my years in one column."*

**A weak indicative anchor, for calibration only.** A salary-aggregator page indicated roughly **₹11.2 L/yr** for a Data Engineer at 1–5 years at this company, and the exact figures are behind a login. Treat that as **indicative and low-confidence**, not as the company's band — and **never repeat this figure to the recruiter or in the interview** (§9). The same page is internally inconsistent: it also shows **16.5** among its latest reported salaries, so treat the *direction* as the signal, not the number. If the eventual number is in that region, it is not a negotiation problem, it is a structural one, and no amount of interviewing fixes it.

### 2.5 Stack mismatch — plan the honest ramp

**The finding.** Reachable evidence points to **AWS** (a disaster-recovery migration of Mumbai→Hyderabad region using Elastic Disaster Recovery, Step Functions and infrastructure-as-code, described as moving core systems to the cloud) and **Microsoft Azure** (Speech and Cognitive Services with NLP, plus in-house data scientists). **No evidence was found of GCP, BigQuery, or Looker anywhere at the company.**

That is an **absence of evidence, not proof of absence** — a large insurer runs many systems and public sources only show what has been announced. But plan for the likely case: your primary platform may not exist there.

**What this changes:**

- **Your differentiator shifts.** If the warehouse is not BigQuery, your advantage is not the specific tool — it is that you have built **end-to-end pipelines with a warehouse and a BI layer**, and that transfers. Say it that way: *"The tool names change; the work doesn't — model the data, orchestrate the load, validate at the boundary, and make the output traceable."*
- **Be ready to name your transferable layer explicitly:** SQL, data modelling, ETL orchestration, data quality and validation, pipeline maintenance. Those are in your verified skills and they are platform-independent.
- **Do not claim** AWS, Azure, Power BI, Snowflake, or Databricks experience. None are in your verified skills. If asked, the honest answer is: *"I've worked in GCP with BigQuery and Looker Studio. I haven't shipped on AWS or Azure. I'd expect the concepts to transfer and the console to be new."*
- **Ask which it is** — question #7 in §1.5. The answer tells you how much ramp you are signing up for.

**The reframe if the stack is unfamiliar:** your value to this role is not that you already know their warehouse. It is that you build **the layer that decides whether the data can be trusted** — which is the same problem on AWS, Azure, or GCP. Lead with that.

### 2.6 Location — probably the hard blocker

ICICI Lombard is **Mumbai-headquartered**. You are **Hyderabad-based** and currently **remote-first**, serving US/UK clients. Indian general insurers' data and analytics roles are ordinarily **office-based**, and this is the single most likely reason this opportunity ends — more likely than comp, more likely than the stack.

**Ask it second, right after the title** (question #3 in §1.5). If the answer is "Mumbai, five days a week", you have your answer in the first five minutes rather than after three rounds. If they offer hybrid or a Hyderabad base, that is a genuinely positive signal worth noting.

**If it is Mumbai on-site,** decide honestly whether you would relocate before you invest further. Do not stay in a process hoping the requirement softens — location requirements at insurers are usually policy, not preference.

---

## §3 — Project priority: what to explain, in what order

He named two things. Map your portfolio onto them and lead with the employer work.

| Priority | Project | Why it's in this slot | Depth to prepare |
|---|---|---|---|
| **1** | **Self-healing data-quality agent** (Black Piano) | He quoted it by name. Employer work. Python + data quality + autonomous resolution. This is the interview. | **Deep — §4.** 5+ minutes unprompted. |
| **2** | **18 automated ETL pipelines → BigQuery → Looker Studio** (Black Piano) | The "data pipelines" half of his sentence. Shows scale, ownership, and warehouse + BI fluency. | **Medium — §5.** 3 minutes, plus one failure story. |
| **3** | **AI insights pipeline + MCP tool** (Black Piano) | The "autonomous AI" half, and the MCP tool is a strong differentiator for a non-technical-stakeholder audience. | **Medium — §5.** 2 minutes each. |
| **4** | **JobAgents** (independent) | Best proof of *engineering discipline* — deterministic scoring, code-enforced anti-fabrication, zero dependencies. Directly relevant if the role involves automation or data governance. | **Medium — §6.** Have the cost-gate and the guard ready. |
| **5** | **Pi Software Python pipelines + 30+ reports** | Proves the Python/data work predates the AI work — this is not a 2026 pivot. | **Light — §6.** 90 seconds. |
| **6** | **AgentSwarm / BugAgents / AI Eco / BrandXY** | Only if asked, or if the interviewer is clearly technical and curious. Do not lead with cosmology papers at an insurer. | **Light — §6.** Know the one-line framing and the honest limits. |
| **7** | **Optum CMS audit (9 years)** | **Do not bury this.** For a regulated insurer it is a differentiator, not a gap. Bring it up in the "tell me about yourself" answer. | **Medium — §7.** |

**The one-line rule:** *lead with what he asked about, prove the Python, then show the audit discipline.*

---

## §4 — The flagship answer: the self-healing data-quality agent

This is the project to know cold. Everything below is grounded in `config/profile.md`; nothing is extrapolated into a claim you cannot defend.

### 4.1 The 90-second version (memorise the shape, not the words)

> "At Black Piano I build the pipelines behind client dashboards. One recurring failure wasn't the numbers — it was **presentation-blocking missing data**: brand domains. Every dashboard renders client logos, and if a brand's domain is missing, the logo doesn't render. Someone had to notice it, hunt the domain down, and fix it in two places — the dataset and the reference lookup table.
>
> That's low-skill, high-frequency, and it silently degrades a client-facing artifact. So I built an agent that resolves it autonomously. It does a reference-table lookup first; if that misses, it falls back to an LLM. When it resolves a domain it writes back to **both** the dataset and the lookup table, so the fix persists and the next occurrence is a cheap table hit. It retries three times on failure, and only escalates by email when it genuinely can't resolve it — so a human sees the residue, not the routine.
>
> The design decision I'd point at is the **write-back to the lookup table**. A naive version fixes the row and moves on, and you pay the LLM cost again next week. Persisting the resolution turns a recurring LLM call into a one-time cost plus a table lookup. The agent gets cheaper the longer it runs."

### 4.2 Architecture — the four questions you will be asked

**Q: Walk me through how it works.**

Layered, cheapest-first:

1. **Detect** — a row needs a domain and doesn't have one.
2. **Reference-table lookup** — deterministic, free, exact. This handles the overwhelming majority and is why the LLM is not on the hot path.
3. **LLM fallback (Gemini)** — only for the residue the table can't answer.
4. **Write-back to both the dataset and the lookup table** — the resolution becomes permanent institutional knowledge.
5. **Retry ×3 on failure**, then **escalate by email for human review** — bounded autonomy with an explicit hand-off.

**Q: Why an LLM at all — why not just a lookup table?**

Because the failure is long-tail. A table only knows what someone already entered; the whole problem is brands nobody has entered yet. The table is the fast path for the known cases, the model is the generaliser for the unknown ones, and the write-back collapses unknown into known over time. **Table-first, model-second, write-back-always.**

**Q: Why does the write-back matter so much?**

Three reasons, and this is the answer that separates you from someone who "used an LLM":

- **Cost decays.** Each resolved brand is one LLM call *ever*, then a free table hit forever.
- **Consistency.** The same brand resolves to the same domain everywhere, because the second lookup is deterministic. A model asked twice could answer differently.
- **Auditability.** The lookup table is a readable record of every domain the system decided on. A reviewer can inspect and correct it. An LLM's in-context reasoning is not auditable after the fact; a table row is.

**Q: Why retry three times, and why email escalation?**

Retries handle transient failure — rate limits, timeouts, a malformed response — where a second attempt genuinely might succeed. They do **not** handle "this brand has no findable domain", and retrying forever would burn budget on an unresolvable case. So the loop is bounded, and the terminal state is **a human gets an email**. The system is autonomous on the routine and explicitly non-autonomous on the residue. That boundary is deliberate: the failure mode of silent wrong data in a client-facing dashboard is worse than the cost of a human reading an email.

**Q: Why is this "self-healing" rather than just "automated"?**

Automation runs a fixed procedure. This one **changes its own future inputs** — the write-back means the system's behaviour on the same input improves permanently. That's the difference, and it's the part I'd defend hardest.

### 4.3 The result, stated without inflation

- Missing brand domains — which block logo rendering in client dashboards — are resolved **without a human in the loop** for the routine case.
- Unresolvable cases are **escalated by email** rather than silently defaulted.
- The reference table **accumulates** resolutions, so repeat cost trends to zero model calls.

**Do not claim:** a resolution rate, a time saving in hours, a percentage reduction in manual work, or a user count. None of those numbers exist in your verified set. If asked *"how much time did it save?"* the honest answer is: *"I don't have a measured figure — I built it because the task was recurring and low-skill, and the durable win is that the reference table now answers most of it deterministically. If I were doing it again I'd instrument the hit rate from day one."* **That answer is stronger than a made-up percentage**, and it sets up §4.4.

### 4.4 Limitations — volunteer two of these

1. **No measured hit rate.** I can't tell you what fraction of cases the table resolves versus the model. I built the mechanism before I built the instrumentation, which is backwards, and it means I can't prove the cost trend I just described — only that the mechanism implies it.
2. **LLM resolution can be confidently wrong.** A hallucinated domain is worse than a missing one, because a missing domain is visibly broken and a wrong one renders the *wrong logo* and looks fine. The write-back amplifies that: a wrong answer persists. There is currently no verification step between "the model answered" and "we wrote it to the table."
3. **The escalation path depends on someone reading email.** If nobody acts, the residue just accumulates.
4. **It solves one specific field.** The pattern generalises; this implementation doesn't. It's a brand-domain resolver, not a general data-quality framework.

**#2 is the best limitation to volunteer.** It shows you understand that a confident LLM answer is the dangerous case, not the missing one — which is precisely the instinct an insurer's data-governance team is hiring for.

### 4.5 What you'd improve with no restrictions

- **Instrument the hit rate first**, so the cost claim becomes a measurement instead of an implication.
- **Add a verification gate before write-back** — a second check that the resolved domain actually belongs to the brand (a fetch, a registry lookup, or a second model with a *falsification* prompt rather than a confirmation prompt). Only verified resolutions get persisted.
- **Make it a general field-resolution framework** — any missing-but-required field, declared as config, rather than one bespoke agent per problem.
- **Add a review queue with a confidence signal**, so low-confidence resolutions go to a human *before* the write-back rather than after a client notices.
- **Track drift**: alert when the escalation rate rises, which is the earliest signal that the table is going stale.

### 4.6 Alternatives not chosen

| Alternative | Why not |
|---|---|
| **Keep it manual** | The task is recurring and low-skill; it consumes attention that belongs on analysis. And the failure is invisible until a client sees a broken logo. |
| **LLM-first instead of table-first** | Cost and latency on every row, and non-determinism on cases a table already answers exactly. Table-first is strictly better where the table has the answer. |
| **Fix the row, don't write back** | The obvious implementation, and the one that makes the system permanently expensive. No write-back means the same lookup recurs forever. |
| **Fail loudly instead of escalating by email** | An unhandled failure in a scheduled pipeline is invisible; nobody reads logs proactively. Email targets a human who can act. |
| **Retry indefinitely** | Some cases are genuinely unresolvable. Unbounded retry converts a data problem into a budget problem. |
| **Block the dashboard on missing domains** | Correctness purism that breaks a client-facing artifact. The right trade is render what you have, resolve in the background, escalate the residue. |

### 4.7 The three follow-ups that will actually come

**"How did you test it?"** — Be honest: *"I tested the resolution paths and the retry/escalation boundary. What I didn't build was a regression suite with a fixture set of known-missing brands — which is exactly the gap that would have given me the hit rate."*

**"What happens if Gemini is down or changes behaviour?"** — The retry ladder absorbs transient failure, and the terminal state is an email escalation, so the pipeline degrades to "human does it manually" rather than "dashboard breaks". A hard provider dependency would be the weakness — and it's why the table-first design matters: the more the table knows, the less the system depends on the provider at all.

**"Could this run on our data?"** — *"The pattern is field-agnostic: detect a missing required field, resolve cheaply first, generalise with a model, persist the resolution, bound the retries, escalate the residue. The brand-domain specifics would change; the four-layer shape wouldn't. What I'd want to know first is whether your reference data is authoritative enough for the deterministic layer — because that's where the cost win lives."*

---

## §5 — Supporting Black Piano answers (have these at 2–3 minutes each)

### 5.1 The 18 ETL pipelines → BigQuery → Looker Studio

**Shape:** 18 automated pipelines feeding BigQuery, surfaced in Looker Studio dashboards across 18 industry sectors.

**The point to make:** *breadth with a single pattern.* Eighteen sectors is not eighteen bespoke systems — it's one pipeline shape parameterised per sector, which is what makes it maintainable. That is the reusable insight: **when the work repeats, the engineering is in the parameterisation, not in the eighteenth copy.**

**Limitation to volunteer:** *"Coverage is a function of the sectors we track, not of the market. And pipeline count isn't a quality metric — eighteen pipelines that nobody monitors are eighteen things that can fail quietly."*

**If asked about orchestration:** be precise. BigQuery scheduled queries, Google Apps Script, and GitHub Actions are in your verified stack. **dbt and Airflow are not** — say so if named.

### 5.2 The AI insights pipeline

Weekly market- and sector-level intelligence generated with ChatGPT, auto-published to a deployed client-facing website, reducing client manual analysis time.

**The point:** it converted a recurring analyst task into a scheduled pipeline with a published output — the value is *cadence*, not the model.

**Careful:** "reduced client manual analysis time" is the verified phrasing. **Do not** attach a percentage or hours figure; none exists. If pressed: *"I can't quantify it — it's a directional claim about removing a recurring manual step."*

**⚠️ Action required — your LinkedIn currently contradicts this.** Your live profile claims *"reduced client manual analysis time by **60%**"*, which is **not** in [../config/profile.md](../config/profile.md) — it survives only in the template file `profile.example.md`. You have confirmed it was left there by mistake and are removing it. **Do it before the interview.** Otherwise a recruiter can read a number on your profile that you are about to decline to defend — and in a recorded, transcript-scored interview that is the worst possible pairing. See [linkedin_blackpiano_rewrite.md](linkedin_blackpiano_rewrite.md).

### 5.3 The MCP tool for non-technical teams

A custom MCP tool that lets marketing and sales generate publication-ready, data-grounded blog posts from a one-line prompt, backed by auto-exported Google Sheets pipelines.

**The point to make — and it's the one that lands with an insurer's digital team:** the hard part was not generation, it was **grounding**. *"A model writing marketing copy is easy. A model writing copy that is actually backed by our data, from a one-line prompt by a non-technical user, is a data-plumbing problem. The auto-exported Sheets pipelines exist so the model reads real numbers rather than inventing plausible ones."*

This is the same instinct as the anti-fabrication guard in §6.1 — **say that out loud.** It is your through-line: *every system I build has a component that decides whether to believe the output.*

---

## §6 — The independent projects (only if asked — keep them labelled as yours)

### 6.1 JobAgents — the one to bring up if the role touches automation or data governance

**One line:** *"A job-sourcing pipeline that refuses to fabricate."*

Two things worth knowing cold:

- **The cost gate goes before the model.** Deterministic scoring computed 22,839 match scores with **zero model calls**, gating only the 155 above-threshold candidates to an LLM. Sources 7,613 jobs / 5,854 distinct roles from 10 sources with 1,759 duplicates merged. **Why it matters to an insurer:** this is the same architecture as a claims-triage or fraud-screening gate — cheap deterministic filter first, expensive model only on the shortlist.
- **The anti-fabrication guard is enforced in code, not in a prompt.** It validates generated text against a ground-truth profile file *before writing to disk*, and it catches **8/8 seeded fabrications** — including a model that attributed independent projects to an employer as employment. **Why it matters to an insurer:** in a regulated business, the question is never "can the model generate the report", it's "what stops the model generating a number that isn't true." The line to say: *"If the rule isn't enforced by something that can reject the output, it isn't a rule — it's a suggestion."*

**Limitation:** the guard catches *structural* violations (invented employers, uncited figures, withheld terms, seniority claims), not confidently-stated false metrics shaped like real ones. Say that before you're asked.

### 6.2 The others, at one line each

| Project | One-liner | Honest limit |
|---|---|---|
| **AgentSwarm** | An autonomous research arena where the audit ledger lives *outside* the agents' writable directory, so the audited cannot edit the audit — 34 runs, 35/35 hash chains intact. | The audit verdict on its own output is **B+ / not publication-grade without the numerical audit**. The two manuscripts are authored by the swarm agents, not by you. Paper 1 is a **Zenodo preprint** — not peer-reviewed. Paper 2 was **not submitted**. |
| **BugAgents** | Two autonomous security-research agents behind an evidence gate: **34 candidate findings refused, 2 promoted.** The refusals are the feature. | Nothing has been submitted to any program. Never name the vendor, asset, or vulnerability class. |
| **AI Eco** | 10 agents under enforceable limits: living memory bounded under 4,000 words, fitness 83.4%, debt-pruning gated at zero false positives. | 83.4% is a self-defined fitness function, not an external benchmark. |
| **BrandXY** | Fine-tuned GPT-OSS-20B (on AMD MI300X) to measure and steer recommendation bias: **76.5% vs 25.5% baseline (+51%)**. | Single-run, no external replication. |
| **Awakening** | Long-horizon autonomy: **1,441 autonomous turns / 1,553 commits**, including **330 turns through an API blackout at 100% CI integrity**. | One run. |
| **mSeat** | Combinatorial seat-allocation simulator validated against published official results — 18,000+ candidates across 59 colleges, within **73 ranks** of cutoff, 90.6% compression. | One phase; a validation exercise, not a deployed product. |

**Do not** open with the cosmology papers at an insurance company. If AgentSwarm comes up, lead with the **ledger integrity and the refusal to overclaim**, not the physics.

---

## §7 — "Tell me about yourself" and the audit angle

### 7.1 The answer that uses all 12+ years

> "I've spent my career on the question of whether data can be trusted.
>
> For nine years at Optum I audited Medicare and Medicaid enrollment transactions for CMS compliance — federal transactions, zero-tolerance quality gates, audit-ready documentation. That's where I learned to treat data quality as a gate rather than a report.
>
> For the last three and a half years I've been on the build side. At Pi Software I built production Python pipelines — an internal package for automated BigQuery access across 10+ client dashboards — and delivered 30+ analytical reports for US and UK clients. At Black Piano I own 18 automated ETL pipelines feeding BigQuery and Looker Studio across 18 sectors, plus the self-healing data-quality agent you mentioned.
>
> Alongside that, on my own time, I build autonomous agent systems — a job-sourcing pipeline, a research arena, a pair of security-research agents. What connects all of it is that the interesting engineering was never getting a model to produce output. It was building the component that decides whether to believe the output."

**Why this works for an insurer:** it makes the audit background the *spine* rather than an awkward pre-2023 chapter, and it positions the AI work as quality infrastructure — which is what a regulated business actually needs.

### 7.2 The Optum bridge — the sentence to have ready

> *"Different regulator, same discipline. CMS audit taught me that a number you can't trace to a source document isn't a number, it's an assertion. I build pipelines with that assumption."*

Then, honestly: **you have no IRDAI or general-insurance experience.** Say it before they ask, and immediately bridge to what transfers — reconciliation, audit trails, defensible numbers, and the discipline of documenting *why* a figure is what it is.

### 7.3 Domain vocabulary — use it correctly or not at all

You will score points for using these correctly and lose more for misusing them. Learn the definitions; do not pretend to operational depth you don't have.

| Term | Correct one-line meaning |
|---|---|
| **GWP / GDPI** | Gross Written Premium / Gross Direct Premium Income — total premium written before ceding to reinsurers; GDPI excludes reinsurance assumed. The headline top-line growth metric, and GDPI is the form Indian insurers usually report. |
| **Loss ratio** | Incurred claims divided by premium earned, for a line of business. The core profitability metric for a general insurer. In insurer disclosures this is the **net** figure — net incurred claims over net earned premium. Gross is computable but is not what gets reported, so expect "net or gross?" as the follow-up. |
| **Incurred Claims Ratio (ICR)** | Claims incurred relative to premium earned over a period — the reported form of the loss ratio in Indian insurer disclosures. Again **net**: net incurred claims over net earned premium, after reinsurance ceded. |
| **Combined ratio** | Loss ratio plus expense ratio. Below 100% means underwriting profit; above means an underwriting loss (typically offset by investment income). |
| **IBNR** | Incurred But Not Reported — a reserve estimate for claims that have occurred but aren't yet notified. An actuarial estimate, which is exactly why its inputs must be auditable. |
| **Claims TAT** | Turnaround time from claim registration to settlement. An operational service metric, and a regulator-visible one. |
| **Persistency / renewal rate** | Share of policies renewed at expiry. A proxy for customer satisfaction and distribution health, measured on premium or policy count. |
| **Fraud / leakage** | Leakage is value lost through unintended over-payment — process error, wrong tariff, duplicate settlement; fraud is the deliberate subset. Analytics teams are usually asked to detect both. |
| **IRDAI** | Insurance Regulatory and Development Authority of India — the sector regulator. Reporting, solvency and disclosure obligations flow from it. |
| **Solvency ratio** | Available solvency margin divided by required solvency margin. IRDAI sets a minimum; a capital-adequacy measure, not a profitability one. |
| **Motor OD / TP** | Own Damage (the insured's own vehicle) vs Third Party (liability to others). Motor TP is a long-tail, regulated, historically loss-making book, and the split matters for reserving. |
| **Bancassurance / distribution mix** | The channel mix through which policies are sold (bank partners, agents, brokers, direct). Drives acquisition cost. |
| **Ceding / reinsurance** | Premium and risk transferred to a reinsurer. Affects net retained risk and net earned premium. **Careful with the causal step:** a *proportional* (quota-share) cession reduces premium and claims together, so it does **not** by itself move the loss ratio. What moves it is **non-proportional cover** (excess of loss, where ceded claims aren't proportional to ceded premium), **ceding commission / profit share**, and **line mix**. Saying "reinsurance lowers our loss ratio" is the tell that you don't know this. |

**The honest positioning:** *"I know the vocabulary and I know how regulated data behaves. What I don't have is general-insurance operating experience — I'd expect to spend my first weeks learning your metric definitions from the people who own them, not assuming mine transfer."* That answer is worth more than false fluency.

---

## §8 — Likely questions and the shape of the answer

| Question | Your answer's spine |
|---|---|
| "Walk me through a project end to end." | §4.1 — the data-quality agent. Detection → table → model → write-back → retry → escalate. |
| "How do you handle missing or bad data?" | Two-layer: **prevent** (deterministic validation, gates) and **recover** (bounded autonomy with human escalation). The data-quality agent is the recover side; the Optum audit discipline is the prevent side. |
| "What's your Python experience?" | Production `Pi-API` package for automated BigQuery access across 10+ dashboards. Then the agent/pipeline work. Name **pandas, FastAPI, PyTorch** — those are in your verified skills. Do not name libraries you haven't shipped. |
| "How do you optimise a slow pipeline/query?" | Partitioning and pruning, pushing filters down, avoiding `SELECT *` and full scans, materialising expensive intermediate results, scheduled aggregation instead of on-demand. Tie it to BigQuery specifically — that's where you've actually done it. |
| "Have you used dbt / Airflow / Spark / Snowflake?" | **No — say no.** Then: *"I've built scheduling and orchestration without them — BigQuery scheduled queries, Apps Script, GitHub Actions. I'd expect to pick up dbt or Airflow quickly; I haven't shipped with them."* |
| "Have you worked on AWS or Azure?" | **No.** Evidence points to this company running AWS and Azure, so expect the question. *"I've worked in GCP with BigQuery and Looker Studio. I haven't shipped on AWS or Azure — I'd expect the concepts to transfer and the console to be new."* Then pivot to the transferable layer: SQL, data modelling, orchestration, validation, traceability. See §2.5. |
| "How do you work with non-technical stakeholders?" | The **MCP blog tool**: a one-line prompt for marketing and sales, grounded in auto-exported Sheets data so the output is real. The engineering is in the grounding, not the interface. |
| "What would you do in your first 30/60/90 days?" | 30: learn their metric definitions and trace three published numbers to source. 60: map the recurring manual work and find where the same failure recurs. 90: automate the highest-frequency, lowest-judgment one — the way the brand-domain agent worked. |
| "Why are you interested in insurance?" | Honest version: regulated, data-dense, and quality-critical — which is where the audit half of your career actually compounds. Do not claim a lifelong passion for insurance. |
| "Why are you looking to move?" | Keep it forward-looking: you've built autonomous data systems on the client side and want a domain where data quality has regulatory weight. Do not criticise Black Piano. |
| "What's your notice period / availability?" | Have the factual answer ready — you're currently employed, so be precise about notice. |
| "Do you have questions for us?" | §1.5. Never say no. |
| "What are your salary expectations?" | §2.4 — ask for their band first, once. |

**The failure modes to avoid in this interview specifically:**

- Claiming a seniority you don't hold. Your titles are Data Analyst. Own it and let the work speak.
- Presenting independent projects as client or employer work.
- Quoting a number that isn't in `config/profile.md` — including any figure from the older blog posts, which contain superseded values.
- Naming the BugAgents vendor, asset, or vulnerability class.
- Saying "we" about solo work.

---

## §9 — Pocket card

**Say:**
- 18 automated ETL pipelines → BigQuery → Looker Studio, 18 industry sectors *(Black Piano)*
- Self-healing data-quality agent — table-first, LLM fallback, write-back to the lookup table, 3 retries, email escalation *(Black Piano)*
- 10+ client dashboards, 30+ analytical reports, Python `Pi-API` package *(Pi Software)*
- 9 years CMS enrollment audit at Optum — data quality as a gate, not a report
- JobAgents: 22,839 scores with **zero model calls**; guard catches **8/8** seeded fabrications
- BugAgents: **34 refused, 2 promoted** — the refusals are the feature
- AgentSwarm: **35/35** hash chains intact; audit verdict **B+ / not publication-grade without the numerical audit**

**Never say:**
- Any title above Data Analyst · any people-management claim
- Any number not in `config/profile.md` (the older blog posts are stale — do not quote them)
- Independent projects as employer/client work
- BugAgents vendor, asset, repository, or vulnerability class
- That BugAgents findings were "disclosed", "accepted", "paid", **or "resolved"** — nothing has been submitted
- Any **production users, revenue, adoption, or customer** claim for JobAgents, AgentSwarm, BugAgents, AI Eco, BrandXY, mSeat or Awakening — none exist
- That you **authored** the AgentSwarm manuscripts — the agent authors are `A001_DarkMatter` / `A002_QuantumCosmos`
- "Peer-reviewed" or "published in a journal" about either manuscript
- Any time-saving percentage or resolution rate for the data-quality agent — there isn't one
- AWS, Azure, Power BI, Snowflake, or Databricks experience — none of it is in your verified skills
- Excel, VBA, or Power Query depth — not in your verified skills
- Any ICICI Lombard financial or compensation figure (the widely-quoted FY2026 GWP number on Wikipedia traces to an unusable citation — do not repeat it), and never the ₹11.2 L aggregator figure from §2.4
- "We" about solo work

**Full forbidden list:** [`outreach_templates.md` §6](outreach_templates.md) — it binds here too.

**Ask before you invest (in this order):** title and level → location and work model → IC or manager → team and reporting line → comp band → who the employer of record is.

**Verify before you send documents:** is Swarnim Vaidya actually at ICICI Lombard, or an agency/RPO? Never send ID, PAN, Aadhaar, or bank details before a JD exists. — §1.3

**The through-line, if you only remember one sentence:**

> *"The interesting engineering was never getting a model to produce output — it was building the component that decides whether to believe the output."*

---

*Companion files: [interview_guide.md](interview_guide.md) (full project deep-dives), [outreach_templates.md](outreach_templates.md) (verified messaging rules), [icici_lombard_research.md](icici_lombard_research.md) (sourced company/role/domain intel), [../config/profile.md](../config/profile.md) (binding ground truth).*
