# Senior Resume — Interview Guide 6 of 6: Question Bank & Pocket Card

**The night-before document.** Cross-cutting questions, the traps, and the one-page card to keep open during the call.

---

## §1 — The opening: "Tell me about yourself"

**Use all 12+ years. Do not start at 2023.**

> *"I've spent my career on the question of whether data and decisions can be trusted.*
>
> *For nine years at Optum I audited Medicare and Medicaid enrollment transactions for CMS compliance — federal transactions, zero-tolerance quality gates, audit-ready documentation. I started there as a Claims Associate and moved into the quality and audit role. That's where I learned to treat data quality as a gate rather than a report.*
>
> *For the last three and a half years I've been on the build side. At Pi Software I built production Python pipelines — an internal package for automated BigQuery access across ten-plus client dashboards — and delivered thirty-plus analytical reports for US and UK clients. At Black Piano I own the pipeline layer: eighteen automated ETL pipelines into BigQuery feeding Looker Studio dashboards across eighteen sectors, plus a self-healing data-quality agent.*
>
> *Alongside that, on my own time, I build autonomous agent systems — a local-first coding agent published on npm, a multi-model evaluation platform, a pair of evidence-gated security-research agents, and an auditable research arena. What connects all of it is that the interesting engineering was never getting a model to produce output. It was building the component that decides whether to believe the output."*

**Then stop.** Let them choose the thread.

---

## §2 — The ten questions you will definitely get

| # | Question | Where the answer is |
|---|---|---|
| 1 | Tell me about yourself | §1 above |
| 2 | Walk me through your strongest project | **BugAgents** — Guide 4 §3 |
| 3 | How do you handle a model producing something wrong? | Guide 5 §1 — the trace, and the gate |
| 4 | What's your experience with RAG vs fine-tuning? | Guide 2 §3.1 |
| 5 | How do you evaluate whether an AI system works? | Guide 2 §3.2 — falsification, not spot-checking |
| 6 | You've never managed a team. How is this senior? | Guide 1 §5 |
| 7 | Rate yourself in Python | Guide 2 §3.3 |
| 8 | You used AI to build all this — isn't that a problem? | Guide 3 §1.5 |
| 9 | What would you do differently? | Guide 1 §5 — instrument the outcome side |
| 10 | Where do you see the limits of this technology? | Guide 5 §1 — the approval/denial asymmetry |

---

## §3 — The traps, and how to avoid each

### Trap 1 — Letting "AI Engineering Leadership" sound like a held title

**The fix:** *"The headline is a direction, not a title claim. My held titles are Data Analyst — that's in the profile section. 'Leadership' means ownership of systems and architecture, not people."*

### Trap 2 — Saying "we" about solo work

**These are yours.** Say "I built", "I designed", "I own". Your resume says it; match it.

### Trap 3 — Inflating the Optum work into claims experience

**The fix:** *"Enrollment transactions — the application and eligibility stage. Not claims adjudication. I'd rather be clear about that."* Say it before they ask.

### Trap 4 — Naming the BugAgents vendor, asset or vulnerability class

**The fix:** *"I'm keeping specifics private until the disclosure process completes, but I'm happy to walk through the verification gate that validated them."* **That answer demonstrates judgement — it is not a dodge.**

### Trap 5 — Claiming production users or adoption

**None exist.** For MyLocalCLI: *"It's published publicly on npm and the portal is live. I'm not claiming adoption figures."*

### Trap 6 — Saying "peer-reviewed" about the AgentSwarm manuscripts

Paper 1 is a **Zenodo preprint** — not peer-reviewed, not a journal. Paper 2 is a **manuscript, not submitted**. The authors are the agents, not you.

### Trap 7 — Sounding risk-averse

**The fix, if any answer makes you sound cautious:** *"I'm arguing for asymmetry, not caution. Push hard where it's safe, be deliberate where it isn't."*

### Trap 8 — Quoting a superseded number

**The fix:** *"That figure is superseded — the current one is X, from the live dashboard."* Common superseded values to watch: 7,533 jobs · 5,784 roles · 32 runs · 32/32 chains · 3,156 tool calls · 182 reports · 209 artifacts · "15+ enterprise dashboards".

### Trap 9 — Claiming React or any tool not on your list

PwC's list includes React. **You have none.** *"I haven't worked with React. My frontend exposure is HTML/JavaScript and static sites."*

### Trap 10 — Claiming a certification

**PMP: prepared, exam not taken.** If it comes up: *"PMP exam preparation, 2024 — exam not taken. I chose to put my time into building AI systems instead, which is when the agent work started."*

---

## §4 — The numbers, all in one place

**Memorise the bolded ones. The rest are reference.**

### Employer work

| Fact | Figure |
|---|---|
| **Black Piano — ETL pipelines** | **18 automated, feeding BigQuery → Looker Studio** |
| **Black Piano — industry sectors** | **18** |
| Data-quality agent | Deterministic lookup → LLM fallback → write-back → **3 retries** → email escalation |
| **Pi Software — client dashboards** | **10+** |
| **Pi Software — analytical reports** | **30+** |
| **Optum — tenure** | **Apr 2014 – Mar 2023** (9 years) |
| Optum — promotion | **Mar 2016**, from Claims Associate |

### Independent systems

| Fact | Figure |
|---|---|
| **BugAgents — gate outcome** | **2 promoted / 34 refused** |
| **BugAgents — findings** | **8 findings, 14 CWE classes** |
| BugAgents — scale | 22 hunt runs / 84 agent turns / **15,317 tool calls** |
| **AgentSwarm — ledger** | **34 runs, 35/35 hash chains intact** |
| AgentSwarm — oracle | **0 violations across 1,254 tool calls**; 0 of 2 agents overclaimed |
| **AgentSwarm — audit** | **22 of 25 claims verified exact**; verdict **B+** |
| **JobAgents — sourced** | **7,613 jobs / 5,854 distinct roles**, 10 sources, 334 companies, 1,759 duplicates |
| **JobAgents — scoring** | **22,839 scores with 0 model calls**; 155 above threshold |
| **JobAgents — guard** | **8/8 seeded fabrications caught** |
| **MyLocalCLI** | npm **v4.0.2**, **42 tools**, **38 skills**, **8 providers**, 5 sub-agents |
| **rAsh Score** | **300 brands, 20 cohorts, 4 dimensions, 4 providers** |
| BrandXY | **76.5% vs 25.5%** baseline |
| Awakening | **1,441 turns, 1,553 commits**, 330-turn blackout at 100% CI integrity |
| mSeat | 18,000+ candidates, 59 colleges, **within 73 ranks**, 90.6% compression |
| AI Eco | 10 agents, memory bounded **<4,000 words**, fitness 83.4% |

### Employment facts

| Fact | Figure |
|---|---|
| Current CTC | **₹12,70,500** (increment letter, effective 1 Jul 2026) |
| Current gross | ₹11,94,270 |
| Notice period | **60 calendar days** |
| Buy-out | Full 60 days, **subject to company approval** |

---

## §5 — Salary and notice-period questions

**"What are your expectations?"**

> *"I'd rather understand the scope and the band first — a senior individual-contributor role and a lead role aren't priced the same. What's budgeted for this grade?"*

**If pushed for a number:**

> *"My current CTC is twelve point seven lakh, and I take home a lakh a month in Hyderabad with no rent because I own the house. So the number isn't the only variable — relocation and cost of living matter as much as the base. On scope, I'd be looking at the band you've mapped this grade to."*

**"What's your notice period?"**

> *"Sixty calendar days. I can request to buy out the full period by paying gross salary in lieu, but that's subject to my employer's approval rather than mine to elect — so I'd plan on sixty and treat anything shorter as a bonus."*

**Do not say you can buy out for 30 days.** You cannot — the buy-out covers the full 60 and needs approval.

---

## §6 — The pocket card

**Keep this open during the call. A glance is fine; reading is not.**

```
POSITIONING
"Nine years regulated healthcare audit, three and a half building data and AI
systems. Both were about whether the answer can be trusted. The interesting
engineering was never getting a model to produce output — it was building the
component that decides whether to believe the output."

SAY
• I own systems end to end — architecture, delivery, controls, audit trail
• I have not had direct reports (state once, flatly, move on)
• 34 refused / 2 promoted — the refusal count is the control working
• The explanation comes from the recorded decision trace, not a model narrating
• Where a result is weak I publish the weakness

NEVER SAY
• Any management title or people-management claim
• A number not in config/profile.md
• BugAgents vendor / asset / vulnerability class
• "disclosed / accepted / paid / resolved" about BugAgents
• Production users, revenue, adoption for any project
• "Peer-reviewed" about either AgentSwarm manuscript
• That you authored the AgentSwarm papers
• React, or any tool not in your verified skills
• "PMP certified"

NUMBERS
18 pipelines | 18 sectors | 10+ dashboards | 30+ reports | 9 yrs Optum
2 promoted / 34 refused | 8 findings / 14 CWE | 15,317 tool calls
35/35 hash chains | 1,254 tool calls | 22 of 25 | B+
7,613 jobs / 5,854 roles | 22,839 scores / 0 model calls | 8/8 fabrications
npm v4.0.2 | 42 tools | 38 skills | 8 providers
300 brands | 20 cohorts | 4 dimensions | 4 providers

COMP & NOTICE
CTC ₹12,70,500 | notice 60 days | buy-out = full 60, needs approval

GAPS — name them first, once, then pivot
• No people management
• No React
• Enrollment audit, not claims adjudication
```

---

## §7 — Final preparation checklist

**The night before:**
- [ ] Read Guide 1 (framework) and Guide 5 (approach) — the two that set the tone
- [ ] Rehearse the §1 opening out loud, three times
- [ ] Rehearse the approval/denial asymmetry (Guide 5 §1) out loud — it is your best 90 seconds
- [ ] Say the BugAgents gate story out loud — 2 promoted, 34 refused
- [ ] Re-read the gaps list and decide how you will say each, in one sentence

**The morning of:**
- [ ] Re-read the numbers table (§4) and the pocket card (§6)
- [ ] Have the resume open in a second window
- [ ] Test camera, mic, connection
- [ ] Confirm the format and platform

**In the room:**
- [ ] Answer first, then explain — never build up to the answer
- [ ] State your criteria on every substantive question
- [ ] Give one concrete example with numbers
- [ ] Name a boundary or limitation before they ask
- [ ] Never say "we" about solo work
- [ ] If you do not know something, say so and reason from first principles out loud

---

## §8 — The three sentences to remember

If you remember nothing else:

> **1.** *"The interesting engineering was never getting a model to produce output — it was building the component that decides whether to believe the output."*

> **2.** *"Auto-approve aggressively behind guardrails; never auto-decline. A wrong approval is a cost you can measure. A wrong denial is a regulatory event."*

> **3.** *"A filter's job is to refuse. A system that never refuses candidates isn't filtering — it's transcribing."*

---

*← Guide 5: Approach · End of series.*

*Companion files: [`icici_health_claims_interview_prep.md`](icici_health_claims_interview_prep.md) · [`pwc_manager_ai_engineer.md`](pwc_manager_ai_engineer.md) · [`resume_variant_comparison.md`](resume_variant_comparison.md) · [`../config/profile.md`](../config/profile.md)*
