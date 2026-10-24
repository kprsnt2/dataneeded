# PwC AC — Manager / Senior Manager, AI Engineering

**Inbound DM from Karthik Balasubramani, Talent Sourcer, PwC AC.**

---

## §0 — Your question, answered

**Send the AI Engineer resume. Not the data one.**

**But the reason to hesitate is not the resume choice — it is that the AI resume currently says, in its own summary line, that you are seeking a *mid-level* role.** You cannot apply for Manager / Senior Manager with a resume that disqualifies you in line 9. §2.

---

## §1 — Why the data resume is the wrong instinct

Your reasoning was *"so that I can say confidently."* I understand it, and it is the wrong trade. Three reasons:

**1. The role's requirements are almost entirely AI-side.** Read their list again:

| PwC's requirement | Data resume shows | **AI resume shows** |
|---|---|---|
| LLM & RAG-based AI solutions | Nothing | **RAG, multi-agent, MCP, evaluation harnesses** |
| Python for backend development | Pipelines only | **FastAPI, Python package, agent runtimes** |
| AI application architecture and delivery | Nothing | **Architecture, guardrails, deployment** |
| Cloud platforms (AWS/Azure/GCP) | **GCP** | **GCP, Cloud Run** |
| React for frontend | Nothing | Nothing |
| Technical leadership and mentoring | Nothing | Nothing |

**The data resume covers one and a half of six. The AI resume covers four and a half.** Sending the data version does not make you safer — it makes you look like you did not read the requirements.

**2. "Confident" is the wrong optimisation.** You would be confident answering questions about a resume that got you filtered out. **The goal is to reach a conversation where you can be honest about the gaps — not to avoid the conversation.**

**3. You have already lived this exact mistake.** You applied to OpenRouter's CLI role without MyLocalCLI on your resume, and only realised afterwards. This is the same error with a different file. **Send the resume that matches the job.**

---

## §2 — The real problem: the AI resume says "mid-level"

Open `resume/Prashanth_Kadasi_AI_Engineer_Resume.md` and read line 9:

> *"Seeking a **mid-level** AI/agent role where audited systems matter more than demos."*

**You cannot send this to a Manager / Senior Manager posting.** A recruiter reading top-down hits that sentence and stops. It is a self-disqualification in the summary.

**Also check the headline (line 2):** *"Data Analyst → AI Systems Engineer"* — fine as a direction, but it does not signal seniority either.

**Fix both before you send anything:**

| Line | Now | Change to |
|---|---|---|
| Headline | *Data Analyst → AI Systems Engineer* | **Data Analyst → AI Engineering — LLM & RAG Systems, Agent Architecture, Python Backend** |
| Summary | *"Seeking a **mid-level** AI/agent role…"* | *"…Seeking an AI engineering role where production-grade delivery and audited systems matter more than demos."* |

**Drop the word "mid-level" entirely.** Do not replace it with "senior" either — just remove the level claim and let the work speak. Your titles stay Data Analyst; you are not inflating anything by *not* calling yourself junior.

---

## §3 — The two gaps you should name, not hide

### 3.1 React

**It is their second bullet and you have none.** React is not in your verified skills, and nothing in your projects uses it.

**Do not** claim it. **Do not** send a resume that implies it. **Do** name it in your reply — see §4.

**How much it matters:** for an *AI Engineer* role, frontend is usually the least-weighted requirement. For a consultancy delivering client applications, it matters more, because you may be expected to ship a working interface. **It is a real gap, and the honest question is whether it is a dealbreaker for them.** Ask.

### 3.2 Technical leadership and team mentoring

**This is the bigger gap, and the same one that came up at ICICI.**

They are hiring at **Manager / Senior Manager** and explicitly want someone who can *"guide engineering teams."* Your profile is unambiguous: **no people-management experience, ever**, and a binding rule against claiming it.

**That does not automatically disqualify you** — consultancies often use "Manager" as a grade, and "mentoring" can mean technical guidance rather than line management. But you must not imply team leadership you have not done.

**The honest framing:**

> *"On the leadership side — I've never had direct reports. What I have done is own systems end to end and work across teams: I built the pipelines and the quality gates at Black Piano, and I've spent three years building and running my own multi-agent systems where the hard part was designing the controls. If the role needs someone to line-manage a team from day one, I'd rather say so now."*

**On a consulting role, that answer is fine.** PwC sells judgement; a candidate who is precise about their own limits reads as lower-risk, not weaker.

---

## §4 — What to send

**Send:** `resume/Prashanth_Kadasi_AI_Engineer_Resume.md` — after the §2 edits.

**With this message:**

```
Hi Karthik,

Thanks for reaching out — the AI Engineering practice is squarely where I've
been building. My updated resume is attached.

Quick context so you can assess the fit accurately:

- LLM & RAG: I've built agent systems with retrieval, tool calling and
  multi-model routing, plus evaluation harnesses. Most relevant: a live
  multi-model evaluation platform (4 providers, 300 brands, 4 scoring
  dimensions) and an open-source CLI coding agent published on npm
  (42 tools, 38 skills, 8 providers).
- Python backend: production pipelines and an internal package for automated
  BigQuery access, plus FastAPI in my agent work.
- Cloud: GCP and Cloud Run in production; BigQuery and Looker Studio.
- AI application architecture: the part I care about is verification —
  I build the layer that decides whether to trust a model's output.

Two things I'd rather flag upfront than have you discover later:

1. I haven't worked with React. My frontend exposure is HTML/JavaScript and
   static sites, not React applications. If the role needs hands-on React
   delivery, I'd want to understand how much of the work that is.

2. I've never had direct reports. I've owned systems end to end and worked
   across teams, but if the Manager level requires line management from day
   one, I'd rather be straight about it now.

Happy to discuss either on a call.

Best,
Prashanth
kprsnt@live.com · +91-9948311964 · https://kprsnt.in
```

**Why volunteer the gaps:**

- **It is the same move that worked at ICICI.** Naming a limitation before they find it converts a weakness into evidence of judgement.
- **It saves you a wasted loop.** If React is a hard requirement, you find out now rather than after three rounds.
- **It reframes the conversation onto your strengths.** The first half of that message is entirely things you have genuinely built.

---

## §5 — The pattern worth noticing

This is now the **third** inbound in a fortnight, and the third with a title question:

| Opportunity | Title offered | Title you hold |
|---|---|---|
| ICICI Lombard | Agentic AI / Product Owner / Senior Manager | Data Analyst |
| **PwC AC** | **Manager / Senior Manager, AI Engineer** | **Data Analyst** |

**Two things follow.**

**1. Your profile is reading as more senior than your title.** Recruiters are finding you on the strength of the agent work and pitching you at Manager level. That is a genuine market signal — your *work* is landing at that level even though your *title* is not.

**2. But your resume contradicts it.** It says "mid-level," it says "Data Analyst → AI Systems Engineer," and it has no leadership language at all. **Every one of these applications is being sent with a document that undersells the thing they are calling you about.**

**That is worth fixing once, properly**, rather than patching per application. Two options:

- **A senior-track variant** — same verified facts, positioned for AI engineering leadership without claiming management: architecture ownership, delivery, cross-functional work, evaluation and governance.
- **Keep the four variants and tailor per role** — more work per application, less coherent.

**I'd suggest the first**, and I can build it: a variant that keeps every number traceable to `config/profile.md`, drops the "mid-level" framing, and leads with architecture and delivery rather than "moving into AI."

---

## §6 — Pocket card

**Send:** the **AI Engineer** resume, after removing "mid-level" from the summary and fixing the headline.

**Do not send:** the data analyst variant. It covers one and a half of their six requirements.

**Volunteer both gaps in the covering message:**
- **No React** — real gap; ask how much of the work it is
- **No direct reports** — never claim otherwise

**Never:**
- Send a resume whose summary says "mid-level" to a Manager posting
- Claim React, team mentoring, or people management
- Swap to the weaker resume to feel more confident — that trades a real conversation for a comfortable rejection
- Forget that this is the third title-vs-resume mismatch in two weeks; fix the resume once
