# Senior Resume — Interview Guide 1 of 6: How to Use This, and the Answer Framework

**What this guide covers:** every claim in `resume/Prashanth_Kadasi_Senior_AI_Engineer_Resume.md`, word by word, with the reasoning, the follow-ups, and the honest limits.

**Six documents:**

| Guide | Covers | Use it for |
|---|---|---|
| **1 — This one** | The framework, the rules, the traps | Read first |
| **2 — Profile & Capabilities** | Headline, PROFILE paragraph, six capability groups | "Tell me about yourself", skills screening |
| **3 — Professional Experience** | Every bullet at Black Piano, Pi Software, Optum | Behavioural and background rounds |
| **4 — Selected Systems** | MyLocalCLI, rAsh Score, BugAgents, AgentSwarm, JobAgents, Also shipped | Technical rounds |
| **5 — Approach** | The four principles | The senior-judgement round |
| **6 — Question Bank** | Cross-cutting questions and the pocket card | The night before |

---

## §1 — The one rule that governs everything

**Every number in this resume is in `config/profile.md`.** That file was reconciled against your live deployed sites. If a figure is not in it, do not say it out loud.

The specific trap: your **engineering blog posts** under `docs/blog/` were written earlier and contain **superseded** figures. Read them for narrative, take numbers from the profile.

If an interviewer quotes an old number back at you: *"That figure is superseded — the current one is X, from the live dashboard."*

---

## §2 — The answer framework: four beats

Every answer in this guide follows the same shape. It is the shape senior interviews reward.

| Beat | Time | What it does |
|---|---|---|
| **1. Direct answer** | 5–10s | Answer the question that was asked, first. Never build up to it. |
| **2. The criteria you applied** | 20–30s | What you weighed and why. **This is the beat that separates senior from mid.** |
| **3. The concrete instance** | 30–50s | One real system, with the numbers. |
| **4. The boundary** | 15–25s | What it does not do, or where you would escalate. |

**Beats 2 and 4 are the ones most candidates skip.** They are the ones being scored at this level.

---

## §3 — The positioning, in one breath

Memorise this. It is the spine of every answer.

> *"I've spent nine years in regulated healthcare operations, auditing federal transactions to CMS standards, and three and a half years building the data and AI systems behind client analytics. What connects them is that in both, the question was never whether the system could produce an answer — it was whether the answer could be trusted. On a regulated decision that's not a feature, it's the design."*

**Why this works:**
- It uses **all 12+ years**, so the audit background is a spine rather than an awkward pre-2023 chapter
- It states the through-line that every project on your resume actually demonstrates
- It sets up the APPROACH section before they have read it

---

## §4 — The five things to say, and the five never to say

### Say

1. **"I own systems end to end."** Architecture, delivery, controls, audit trail. This is the senior claim, and it is true.
2. **"I have not had direct reports."** State it plainly, once, and move on. It is in your resume; hiding it makes it look like a problem.
3. **"The refusal count is the control working."** 34 refused, 2 promoted. Your best single line.
4. **"The explanation has to come from the decision trace."** Your strongest technical position.
5. **"Where a result is weak I publish the weakness."** Nobody else says this.

### Never say

| Never | Because |
|---|---|
| Any **management title** you did not hold — Senior Manager, Lead, Head of | Your held titles are Data Analyst. This is binding. |
| Any **people-management** claim — "led a team", "managed engineers", headcount, budget ownership | There is none. It is in your resume as an explicit absence; contradicting it is fatal. |
| A number not in `config/profile.md` | Superseded figures are actively misleading |
| BugAgents findings described as **disclosed, accepted, paid, resolved or submitted** | They are submission-ready drafts. Nothing has been submitted. |
| The BugAgents **vendor, asset, repository or vulnerability class** | Withheld pending responsible disclosure |
| **Production users, revenue, adoption or customers** for any independent project | None exist |
| **"PwC certified me"** or any credential you do not hold | Including PMP — prepared, exam not taken |
| That you **authored** the AgentSwarm manuscripts | The authors are `A001_DarkMatter` / `A002_QuantumCosmos` |
| **React** or any tool not in your verified skills | PwC's list includes React; you have none. Say so. |

---

## §5 — The three hardest questions you will get

Prepare these properly. They come up in every senior interview, and they are the ones this resume invites.

### "You've never managed a team — how is this a senior role?"

> *"Fair question, and I'd rather answer it directly than talk around it. I haven't managed people. What I have done is own systems end to end — architecture, delivery, the controls, and the audit trail — and I've done it in a regulated environment where the decisions had to be defensible to an external auditor.*
>
> *The way I'd describe the level: I'm the person who decides what the system should do, what it must refuse to do, and how you'd prove afterwards that it behaved. That's architecture and governance work. What I haven't done is run a team, and I wouldn't claim it."*

**Then stop.** Do not over-explain. The answer is strong because it is bounded.

### "Which of these projects is your strongest work?"

> *"BugAgents, and not because of the security findings. Because it's the one where I built the gate that decides whether to believe the agent — four conditions that must all hold, and the outcome was 2 promoted against 34 refused. The refusals are the number I'd defend hardest. A filter that promotes everything it's given has a refusal count of zero and no verification at all. It would look more productive on every dashboard and it would be worthless."*

### "What would you do differently?"

> *"Instrument the outcome side first. In JobAgents I measured the top of the funnel to the unit — 22,839 scores — and the bottom not at all. I can tell you every score and I cannot tell you whether any of it worked. That's the gap, and it's the first thing I'd fix in any system I build now."*

**That answer is unusually strong** because it is a real limitation you found yourself, and it demonstrates the instinct the role needs.

---

## §6 — How to handle the gaps

Three gaps will come up. Have the honest version ready for each.

| Gap | The answer |
|---|---|
| **No people management** | *"I haven't had direct reports. I've owned systems end to end and worked across functions."* Say it once, then move to what you have done. |
| **No React** (PwC's list) | *"I haven't worked with React. My frontend exposure is HTML/JavaScript and static sites. If the role needs hands-on React delivery, I'd want to understand how much of the work that is."* |
| **No Indian health-insurance claims operations** | *"I'm not a claims operator and I won't pretend to be. What transfers is nine years of regulated audit discipline — decisions traceable to a rule and defensible to an auditor. That's the same requirement the JD puts on automated decisions."* |

**The principle:** name the gap before they find it, in one sentence, then pivot to what you do have. **Volunteering a limitation is the fastest credibility you can buy**, and it pre-empts the question.

---

## §7 — The through-line, if you remember only one sentence

> *"The interesting engineering was never getting a model to produce output — it was building the component that decides whether to believe the output."*

Every system on your resume is evidence for that sentence. Every answer should return to it.

---

## §8 — Practical preparation

**Read order:** this guide → 2 (Profile) → 4 (Systems) → 3 (Experience) → 5 (Approach) → 6 (Question Bank).

**Rehearse out loud:** the positioning (§3), the three hard questions (§5), and the four APPROACH principles (Guide 5).

**Keep open during the call:** a one-page trigger sheet:

```
1. M. Pharmacy — clears medical-discipline requirements
2. Optum: Claims Associate (2014-16) → CMS enrollment audit (to 2023)
3. 18 ETL pipelines → BigQuery → Looker Studio (Black Piano)
4. BugAgents gate: 4 criteria, 2 promoted / 34 refused
5. AgentSwarm: 35/35 hash chains, ledger outside writable dir
6. JobAgents: 22,839 scores, 0 model calls, 8/8 fabrications caught
7. rAsh Score: 300 brands, 20 cohorts, 4 models
8. MyLocalCLI: npm v4.0.2, 42 tools, 38 skills, 8 providers
```

**Never read from a script.** A glance at a trigger sheet is normal; reading is not.

---

*Guide 2: Profile & Capabilities →*
