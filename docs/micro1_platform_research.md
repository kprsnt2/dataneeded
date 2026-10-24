# micro1 — Platform, Interview Format & Role Intel

**Prepared for:** Prashanth Kumar Kadasi (Hyderabad) — two live micro1 interview invitations
**Prepared by:** micro1-researcher (shared task `task-3`)
**Date:** 2026-10-12
**Scope:** micro1 the *platform* only. ICICI Lombard company research is a separate brief.

---

## 0. Evidence grading — read this first

Every factual claim below carries one of three tags. The distinction is the point of this brief.

| Tag | Meaning | How to treat it |
|---|---|---|
| **VERIFIED** | Stated by micro1 itself (website, legal pages, official subreddit posts by staff), or by the candidate's own invitation screenshots. | Treat as platform policy / fact. |
| **ANECDOTAL** | Individual candidate testimony (Reddit, blogs). Unverified, un-audited, self-reported. **Not policy.** | Use as a *hypothesis about the test*, never as a rule. |
| **UNVERIFIED** | Could not confirm from any source. | Assume nothing. Ask on the day. |

**Why this matters for this specific brief:** a confident wrong answer about the interview format is worse than "could not confirm." The candidate walks into a timed, recorded, auto-scored interview. If he prepares for a *coding test* because a Reddit post said so, and the actual test is a *rubric-grading exercise*, he loses the slot. Where the evidence is only ANECDOTAL, this brief says so explicitly and says what to do instead.

**Method / access note.** `web_search` was unavailable (no API key). All findings come from direct `web_fetch` of specific URLs. Reddit is reachable only via the Redlib mirror `red.artemislena.eu`; `www.reddit.com`, `old.reddit.com`, `glassdoor`, `trustpilot`, `ycombinator`, `web.archive.org`, `inc.com`, `businessinsider.com` and DuckDuckGo were DNS-blocked from this environment. **Consequence: Glassdoor and Blind were never reached.** That is a real gap, recorded in §I.

**Primary evidence used (not web):**
- `docs/assets/micro1_data_analyst_43min.png` — 43-minute interview invitation, topics listed.
- `docs/assets/micro1_ai_agent_evaluator_20min.png` — 20-minute interview invitation, topics listed.
- `config/profile.md` — candidate ground truth (used only for fit commentary in §E/§J).

---

## 1. Bottom line — what should change how he prepares

Six findings that alter preparation. Detail and sources follow.

1. **The interviewer is a voice AI named Zara, not a human, and it is auto-scored in real time.** VERIFIED by micro1. "A real-time result indicating whether you meet micro1's global certification criteria" — he may get a pass/fail verdict the moment he finishes. There is no human to charm. → Prepare for a *machine-readable* answer structure.
2. **A pause can be read as "answer finished."** ANECDOTAL but reported independently by several candidates. One candidate's own summary: *"Zara would mistake a pause as 'you're done answering' and so it's best to say 'let me think about that for a minute'."* → He must **narrate his thinking out loud** rather than go silent to compose an answer. This is the single highest-value behavioural change.
3. **He can rehearse on the real product, free, before the real thing.** VERIFIED. micro1 publishes free AI mock interviews at `interview.micro1.ai/mock-interview` and a prep library at `micro1.ai/interview-prep`. Multiple candidates report running the mock 2–3 times first. → **Do this.** It de-risks the format more than any amount of reading.
4. **The rubric rewards a specific vocabulary that he already owns but may not be using.** micro1's own post-interview feedback email (leaked verbatim by a candidate, §E) praises "rubric adherence", "documenting rationale for each decision", "severity taxonomy", "calibration sets or inter-rater reliability", "how to score partial correctness". These are literally his AgentSwarm/BugAgents concepts. → He should *say those exact terms*.
5. **His two invitations differ in a way that matters.** The 20-minute "AI Agent Evaluator" set (Following Detailed Instructions Exactly / Hands-On Use of AI Tools / Judging When to Step In + "Custom questions defined for the job") is instruction-following and tool-use flavoured. The 43-minute Data Analyst set is quality-assurance and judgement flavoured. → Two different answer banks, not one.
6. **The interview is a *gate*, not a job.** VERIFIED. Certification ≠ placement. micro1 says plainly: *"Certification does not guarantee immediate placement."* Many candidates clear the interview and then sit in "Hiring Manager Reviewing" for up to 30 days. → Treat a pass as *eligibility*, and keep the job pipeline running in parallel.

---

## A. What micro1 is

### A1. Company facts — VERIFIED

| Fact | Value | Source |
|---|---|---|
| Legal entity | micro1, Inc. | Privacy Policy footer |
| HQ address | 655 Montgomery St, San Francisco, CA 94111 | Privacy Policy §15 |
| Self-description | "Data lab to train frontier models & evaluate agents" | micro1.ai homepage |
| Products | **Realm** (RL environments for AI labs), **Cortex** (agent evaluation platform), **Robotics** (expert-demonstrated robotics data) | micro1.ai nav |
| Research | Publishes benchmarks; `PersonalAgentBench` is a public agent benchmark | micro1.ai/research |
| Business model | Sells expert human data, evaluation environments, and evaluation services to frontier AI labs and enterprises | micro1.ai; Cortex page |
| Revenue signal | TechCrunch (2026-08-20): "AI data startup micro1 reaches $500M gross run rate amid AI training boom" | TechCrunch headline + micro1 newsroom |
| Growth claim | CEO Ali Ansari, Antler podcast: "$7M to $700M+ ARR in ~2 years" | micro1 community/forum listing |
| Official email domains | `@micro1.ai`, `@micro1.io`, `@micro1.co` — "All are verified and used for communication about interviews, certification, and projects" | micro1.ai/expert FAQ |
| Talent platform | `talent.micro1.ai` (dashboard/login); interviews at `interview.micro1.ai`; jobs at `jobs.micro1.ai`; referrals at `refer.micro1.ai` | micro1.ai nav + job links |
| Official subreddit | `r/micro1_ai` — 32.3k members, staff-posted flair "News & Updates", active Community Managers | Redlib mirror of r/micro1_ai |
| Payment rails | Deel (contracts/payouts), Hubstaff (time tracking), Slack (project comms), micro1 Google Workspace email | "New to micro1? Start here!" staff post |

**Verdict on legitimacy (company level):** micro1 is a **real, well-capitalised, venture-scale company** with named executives, a physical address, mainstream press coverage (TechCrunch, Forbes, CNN, WSJ, LA Times, CNBC, Business Insider, NBC Bay Area), and a 32k-member community it staffs with employees. The "is micro1 a scam" genre exists and is loud (§G), but the *"fake company that doesn't exist"* hypothesis is **false** and should not drive his decisions.

### A2. What the "interview" actually is, in micro1's funnel — VERIFIED

micro1's own published pipeline:

```
Apply to a role  →  AI interview with Zara  →  Certified (needs government ID)
   →  Vetted talent pool  →  Hiring Manager Review (client)  →  Selected
   →  Contract + Slack + Hubstaff + Deel  →  Onboarding  →  Project work
```

Key VERIFIED statements:
- *"Every applicant goes through an AI-driven interview with our AI Interviewer, Zara, which evaluates your communication skills, logical reasoning, and role-specific skills."*
- *"Our interview will also have role-specific challenges; for example, Software engineering candidates complete a live coding challenge, and Human data experts complete task-based exercises simulating real AI training workflows."*
- *"After successfully completing the interview, you'll be required to verify your identity using a government-issued ID (passport, driver's license, or national ID)."*
- *"Certified candidates typically get an update on their application status within 30 days of completing their interview."*
- *"Certification does not guarantee immediate placement."*
- **Retake/feedback:** *"In case you didn't perform well for an AI interview, you will get detailed feedback on your AI interview performance."*

**So: the interview is a certification gate feeding a talent marketplace, not a job interview for a named employer.** This is the single most important structural fact. His "AI Agent Evaluator" interview is not necessarily for one employer — it may be certifying him into a pool.

### A3. The Cortex product — why it explains the 20-minute interview — VERIFIED

micro1's own Cortex page describes the work his role would feed:

> Cortex — "Evaluate, improve, and monitor AI agents with expert human judgment, derived from real workflows."
> 1. **Evaluation design** — "Define success criteria, **rubrics**, and **scoring** for the agent's task"
> 2. **Failure diagnosis** — "Domain experts review agent outputs and identify **where, why, when, and how the agent fails**"
> 3. **Expert training data** — targeted data produced by experts to address failure modes
> 4. **Monitor reliability** — re-evaluate as models/prompts/rules change
> Differentiator claimed: *"Human expert review beyond automated evals and LLM-as-judge."*

A micro1 engineering post adds the vocabulary used internally: *"isolate that exact trace, **grade the reasoning chain**, and correct the failure mode"*; *"graded multi-turn traces, your **failure taxonomies**, your expert feedback loops"*; *"Continuous Calibration."*

**This is the actual job behind the 20-minute interview.** His topics map 1:1 onto Cortex's four steps (see §D).

---

## B. Interview format & mechanics

### B1. What his own invitations say — VERIFIED (primary evidence, screenshots)

Both invitations share identical mechanics wording:

> "Please note that this interview will take **~43 minutes** / **~20 minutes** with **each question having a limited time for a response**. You will answer by **speaking, or typing**. Ensure you're in a **quiet spot with a stable internet connection**. This interview will be **recorded and available in your profile link**."
> "Please **don't refresh the page** during the interview."

**Interview A — Data Analyst track, ~43 min** — topics:
`Data quality review & QA validation` · `Judgment under ambiguity & documentation of rationale` · `Rubric-based evaluation & guideline adherence` · `Spreadsheet proficiency (baseline)` · `Error & Edge-Case Detection`

**Interview B — AI Agent Evaluator track, ~20 min** — topics:
`Following Detailed Instructions Exactly` · `Hands-On Use of AI Tools` · `Judging When to Step In` · plus **"Custom questions defined for the job"**

**Verified mechanics extracted from the screenshots themselves:**
- Duration is an estimate, per-question timers are real ("each question having a limited time").
- **Speaking OR typing is an explicit, offered choice** — this is stated by the platform, not inferred.
- It is recorded; the recording is retained and reachable from his profile link.
- Refresh breaks the session (stated as a warning).

### B2. Officially documented format — VERIFIED (micro1's own AI Interview Guide)

From `micro1.ai/ai-interview-guide`:

- *"A conversational interview with our AI recruiter, Zara."*
- *"Available on demand—complete it anytime, from anywhere."*
- **Types of questions asked:**
  - Open-ended technical questions based on your chosen role
  - Scenario-based questions to evaluate how you think, problem-solve, and communicate
  - Coding challenge for technical roles
  - **Human data exercise for annotator roles**
- **What you get:**
  - Immediate access, on demand
  - *"A **real-time result** indicating whether you meet micro1's global certification criteria"*
  - *"The option to request feedback if certification is not achieved"*
- **How to prepare (micro1's own advice):**
  - *"Choose one core skill or job type you want to be evaluated on."*
  - *"Use our Interview Prep tool to simulate interviews before taking the real one."*
  - *"Optionally, create customized questions in advance to better showcase your expertise."*
  - *"Watch the short demo video to see exactly how the process works."*

From `micro1.ai/interview-questions` (official question bank):

- *"No two candidates receive the same questions."*
- *"Zara, our AI recruiter, adapts to your background and evaluates how you think, solve problems, and communicate."*
- *"The level of difficulty and scope varies depending on your field and experience."*
- Published **soft-skills** examples (directly relevant to "Judgment under ambiguity"):
  - *"Describe a time you disagreed with a team member—how did you handle it?"*
  - *"How do you manage uncertainty when making decisions?"*
  - *"Tell me about a project where communication broke down. What would you do differently?"*
- Published role examples show the expected answer *depth*: multi-part, trade-off-aware, architecture-level questions (e.g. Full-Stack: "Explain the trade-offs between different architectural patterns … and discuss their impact on scalability, maintainability, and deployment complexity").

From `micro1.ai/interview-prep/data-analyst-interview-questions` — micro1 publishes **10 sample Data Analyst questions**. Themes: advanced data cleaning in large multi-source datasets; statistical analysis; **handling outliers and missing values** ("Senior analysts **document these choices to maintain reproducibility**"); visualization; normalization/transformation; model robustness; **automating repetitive cleaning**; tool selection; advanced statistics; **QA measures** ("data validation checks, automated unit tests, regular audit trails, peer code reviews, dashboard stress-testing, and maintaining **thorough documentation**").

> **Read that last one again.** micro1's own published Data Analyst question list uses the phrase "document these choices to maintain reproducibility" and "maintaining thorough documentation" — which is the same skill his invitation calls **"documentation of rationale."** His invitation topics are not arbitrary; they track micro1's published question bank.

### B3. Interview anatomy — ANECDOTAL (multiple independent candidates, converging)

The following is candidate-reported, **not** platform policy. It is included because 6+ independent accounts converge, which makes it a reasonable working model.

Consensus shape of a Zara interview:

1. **Identity / intro** — Zara asks him to introduce himself.
2. **Adaptive drill-down** — Zara generates follow-ups *from his own intro and resume*. One candidate: *"Zara typically extracts context from how you finish your intro to generate its follow-up questions."* Another: *"it asks you to introduce yourself and then dynamically navigates from there, exploring the parts of your past experience."*
3. **Scenario questions** — increasingly specific hypotheticals; Zara comments on answers, then either probes deeper or moves on.
4. **A written / task portion** — several candidates describe an *"interview portion and a test portion."* A micro1 Community Manager confirmed in-thread: *"this is role specific, some may have domain specific assessments while others may not have. You can check this information right before interview starts as it clearly mentions skills assessed, duration, etc."* — so **the pre-interview screen tells him whether a test portion is included. He should read it carefully before starting.**
5. **Result** — immediate verdict pane, and/or dashboard status.

Corroborating details:
- **Transcript is live on screen.** *"Its questions are transcribed."* Also: *"the transcription is dynamic, and while Zara is speaking, you won't be able to navigate through its previous questions/comments"* — **he cannot scroll back to re-read a question.**
- **He can ask Zara to rephrase.** *"if you don't understand something, you can ask it to rephrase the question"* — and one candidate explicitly advises: *"if you don't understand something or miss part of a question, ALWAYS ask for rephrasing."*
- **Speech pace is fast.** Reported independently at least four times: *"She speaks very fast making it difficult to instantly understand"*; *"Zara generally speaks pretty fast"*; *"a consistent speaking tone and pace for 30–50 minutes."*
- **A timer is visible.** *"There was a timer which I did not notice until about midway through."*
- **"Partial interview"** — a real concept: if he is already certified on some of a role's skills, the interview can be shortened to only the un-vetted skills. Candidates report this behaviour changing over time. Status: **ANECDOTAL, and currently in flux** — several users in Oct 2026 report partial interviews no longer being offered.
- **Immediate disqualification is possible.** One candidate: *"Immediately after the interview, the pane popped up stating I didn't qualify."*

### B4. Mechanics he asked about — status of each

| Question | Answer | Grade |
|---|---|---|
| Can he choose speaking vs typing? | **Yes — the platform says so.** "You will answer by speaking, or typing." Note the written portion is *not* optional where the role has one. | **VERIFIED** |
| Per-question time limit? | **Yes.** "each question having a limited time for a response." Visible timer per candidates. | **VERIFIED** (limit exists) / **ANECDOTAL** (a timer is displayed) |
| Retake? | micro1 does **not** publish a retake policy. One candidate reports: *"micro1 allows you to either retry the same role after 30 days or immediately apply to a different role."* Treat as unconfirmed. | **UNVERIFIED** |
| Proctored? | micro1's Candidate Privacy Policy explicitly names *"information collected from our **proctoring tools** to assess the integrity of your interviews."* A candidate reports being asked to **screen-share** before starting, and that **pen and paper was disallowed** ("it counts as cheating"). Whether screen-share applies to his two roles is unconfirmed. | **VERIFIED** (proctoring exists in policy) / **ANECDOTAL** (screen-share, no-pen-and-paper) |
| What breaks a recording? | **Refreshing the page** (stated on his own invitation). Separately, a long-running official megathread documents Zara freezing, not progressing after the intro, lag, and repeating questions. Official remedies: wired Ethernet, no public Wi-Fi, pause other bandwidth use, and **retry in Chrome incognito or Firefox Private**. Multiple candidates report **Chrome getting stuck and Firefox working**. | **VERIFIED** (refresh; official troubleshooting) / **ANECDOTAL** (browser-specific outcomes) |
| Technical requirements | Quiet space + stable internet (his invitation). Official: wired connection preferred, avoid public Wi-Fi. Practical: camera and mic set up before starting. | **VERIFIED** |
| Does he get feedback if he fails? | **Yes, officially.** "The option to request feedback if certification is not achieved." A candidate reproduced a genuinely detailed feedback email (§E). | **VERIFIED** |

### B5. Format — what is still genuinely unknown

- Whether his specific 43-min and 20-min interviews include a **written test portion** in addition to the conversational part. **The pre-interview screen states "skills assessed, duration, etc." — he must read it before clicking start.**
- Whether the 43-minute one includes a **spreadsheet task** (the topic says "Spreadsheet proficiency (baseline)", which implies an interactive component, but nothing confirms the mechanism).
- Whether either is **screen-shared/proctored**.
- Exact **number of questions** and **per-question seconds**.
- Whether the **43-minute estimate includes the written portion**.

---

## C. What candidates report — ANECDOTAL

**All of §C is unverified candidate testimony. None of it is micro1 policy.**

### C1. Strongly positive accounts
- A family-law attorney (50 y/o) expected the worst, then: *"I got on camera and there isn't like an AI model speaking it was just an icon… it was like speaking to a colleague… After each question, I was given feedback… I was actually disappointed when the time ran out."* She **asked if she could take notes and was told yes**, and was **not** asked to pan the room for a script. She did not get the role, but: *"I got an option to request feedback and received a detailed explanation… I agree with the assessment."*
- A certified candidate: *"I kept my English very very basic"* and used Zara's own feedback comments to build domain vocabulary mid-interview.
- *"Zara, the AI Interviewer, was honestly better than any human who has ever interviewed me. She understood everything I said, responded thoughtfully, and even gave positive feedback on my answers"* (quoted on micro1's own reviews page).
- *"It's helping me overcome the issues I had — lack of clarity in expressions and communication. Thanks Zara."*

### C2. Negative accounts — and the specific failure modes
- **Fast speech + accents.** *"She speaks very fast… Her pronunciation/diction was off in a few places… Terms referenced were specialist terms relating to data labelling/annotation that I had never heard of."*
- **Domain vocabulary, not domain skill, decides.** An experienced SDR was *"immediately 'not qualified'"*: *"my difficulty answering those questions wasn't because I don't know how to sell. It was because I was being asked to describe my sales experience in a language I don't speak."*
- **Questions drift off the job description.** *"I've noticed a fairly consistent gap between the job descriptions and the questions Zara asks."* Another: *"I was asked about areas that weren't mentioned in the required list."* A candidate was asked to solve **Fibonacci and geometric sequences verbally with no pen and paper**.
- **Jargon-heavy register.** *"The questions… were also very 'jargonistic' and super scholarly."*
- **Breadth, not depth.** *"Human interviews typically unfold through multiple layers, gradually move from breadth to depth… ZARA AI interview is compressed into a single sitting."*
- **Silence is dangerous.** *"Zara can interpret the silence as the end of your answer and prompt you to continue."*
- **Zero transparency on scoring.** *"Was it my pronunciation? Recording quality? One specific answer? An automated score? A quota? Was any human ever involved?"*
- **Positive in-interview feedback does not predict outcome.** *"The conversational AI may inform you that your rationale is solid… such statements appear to bear little if any relevance to the certification determination."*
- **Platform instability.** Zara freezing mid-interview, requiring a full restart: *"I had to take the interview twice because the first one got disconnected at their end exactly when I finished the audio interview and when it was time to take the written test."*
- **A writing-task dead end.** *"Zara interview insists on writing where there's nowhere to write"* — the bot demanded a typed answer with no input field visible. **Mitigation: if he is asked to type and sees no field, say so aloud and ask for a rephrase/alternative rather than burning the timer.**

### C3. Volume/outcome statistics from candidate testimony
- One candidate's tally: **12 interviews — 6 "didn't qualify", 4 "not selected", 2 stuck in HMR >15 days.**
- Another: *"After 18 rejections and 40 vetted skills, I finally got an offer!"*
- Reported timelines from interview → offer: **2 days** (one case), **~1 week** (another), **30 days** (documented upper bound, and the official ceiling).
- Status vocabulary candidates see: `Under Review` → `Did Not Qualify` / `Not Qualified`, or `Hiring Manager Reviewing (HMR)` → `Selected`. Emails reported: *"Great Work on Your Interview"*, then a contract-signing email.
- **"Vetted skills"** accumulate on his dashboard, graded **Mid-level** and **Senior**; one candidate found graded skills in their **exported personal data** that never appeared on their profile.

### C4. What candidates say actually works (consensus prep advice)
1. **Do the official mock interview 2–3 times.** *"I did three rounds of one of the mock interviews available on the Micro1 website to understand how Zara works."*
2. **Use STAR**, and put **concrete specifics in the "Action" step** — named tools, named columns, named thresholds.
3. **Seed the intro deliberately.** Finish the intro with the experience you *want* probed.
4. **Answer in numbered points**, ~2–3 minutes each.
5. **Never go silent** — say "let me think about that for a moment", or ask for a rephrase.
6. **Ask for rephrasing freely** — it is allowed and it is the main recovery mechanism.
7. **Mention domain terminology** even when experience is adjacent: a micro1 Community Manager replied to a complaint about jargon with: *"the 'jargon' is actually a requirement to train the AI models, and thats why its important."* (That is a staff statement — close to policy.)
8. **Don't apply to several near-identical roles at once** — let skills get vetted first so later interviews can be partial/faster.
9. **Browser fallback:** Chrome → Firefox if Zara hangs.

---

## D. The AI Agent Evaluator role — what the work actually is

### D1. The role exists at micro1 — VERIFIED
- **"AI Agent Task Evaluator"** was posted by micro1's official Reddit account, week of **2026-08-31**: **pay $20–$45/hour**, referral bonus $100. Link: `jobs.micro1.ai/post/873d9cd8-0a0f-4875-acc3-87d5502cce7a`
- Adjacent evaluator roles posted by micro1 in the same period:
  | Role | Advertised pay |
  |---|---|
  | AI Agent Task Evaluator | $20–$45/hr |
  | AI Evaluation Analyst | $20–$30/hr |
  | AI Evaluation Specialist | $22–$70/hr |
  | Visual Evaluation Specialist | $20–$70/hr |
  | LLM Red-Teamer | $40–$65/hr |
  | AI Jailbreak & Prompt-Injection Security Expert | $50–$90/hr |
  | AI Productivity Specialist / AI Workflow Specialist | $30–$90/hr |
- A candidate in `r/AiTraining_Annotation` posted **"Just got a Micro1 AI Evaluator contract"** (19 upvotes) — confirming the title is issued as a real contract.

### D2. Day-to-day — from micro1's own product descriptions — VERIFIED
Derived from the Cortex page and micro1's "AI Evaluation Layer" post:
- **Grade multi-turn agent traces** — read the full reasoning chain, not just the final answer.
- **Write and apply rubrics / scoring criteria** — "Define success criteria, rubrics, and scoring for the agent's task."
- **Diagnose failures** — identify *where, why, when, and how* the agent failed; build a **failure taxonomy**.
- **Produce targeted training data** from the highest-value failures.
- **Monitor reliability** as prompts/rules/models change.
- **Judge when automated evals are insufficient** — the product's stated differentiator is *"Human expert review beyond automated evals and LLM-as-judge."*
- **flow-qc** (micro1's newer pipeline) "evaluates performance, finds the highest-value failures, and routes them back to experts for review."
- **flow-gen** "turns expert judgment into new environments, rubrics, variations, and **edge cases**." ← note: *edge cases*, matching his "Error & Edge-Case Detection" topic.

### D3. Industry-standard framing of the title — corroborated
The industry meaning matches micro1's: evaluating agent traces, writing rubrics, red-teaming, judging model outputs, and labelling preference data are the standard components of an "AI agent evaluator"/"AI evaluation specialist" role across AI-data companies. micro1's own listings for *LLM Red-Teamer* and *AI Jailbreak & Prompt-Injection Security Expert* confirm the red-teaming variant is a sibling role, not the same one. **No single authoritative industry definition was retrievable in this environment** — this section is assembled from micro1's product pages rather than a standards body. Grade: **VERIFIED for micro1's own definition; UNVERIFIED for a universal industry definition.**

---

## E. Rubric adherence & rationale documentation as assessed skills

This is the highest-leverage section of the brief, because micro1's own feedback language is available.

### E1. The primary artifact — micro1's actual feedback email — ANECDOTAL (leaked by candidate), but unusually informative
A candidate for **AI Evaluation Specialist** reproduced micro1's post-rejection feedback email verbatim. It is the closest thing available to a published rubric. It praised:

> - *"strong **risk-based thinking** in AI output evaluation and quality assurance, effectively highlighting the importance of **intent alignment, factual accuracy, hallucination avoidance, and rubric adherence**"*
> - *"treating **factuality and safety as non-negotiable**… awareness of different **severity levels** across domains"*
> - *"**structured approach to scoring using evaluation guidelines**… clear focus on **rubric-driven assessment, consistently mapping criteria and documenting rationale for each decision**, which reflects your commitment to fairness, consistency, and safety"*
> - *"solid **editorial judgment**… prioritizing accuracy and **user impact**, especially when handling high-stakes content"*
> - *"ability to provide specific, actionable feedback focusing on **what's wrong, why it's wrong, and what to do next**"*

And it flagged as **areas for improvement**:
> - *"a consistent, scalable **severity taxonomy** or mechanisms to ensure evaluation consistency, such as **calibration sets or inter-rater reliability**"*
> - *"structured scoring with more concrete examples, such as providing **templates for note-taking** or detailing **how to score partial correctness**"*
> - *"**microcopy craft** — such as **tone calibration, brevity, and user context**"*

**This is a vocabulary list.** It is what micro1's scoring layer rewards. Grade ANECDOTAL (one leaked email) but it is internally consistent with micro1's published question bank and its Cortex product language — three independent sources agreeing raises confidence materially.

### E2. What "documentation of rationale" means in this domain
Synthesising the above with micro1's published Data Analyst question list and Cortex's process:

**Documenting rationale = writing, alongside every judgement, the minimum set of things an independent reviewer would need to reproduce your call:**
1. **Which criterion** from the rubric you applied (name it).
2. **What you observed** that triggered it (cite the specific span, cell, value, or trace step — not "the answer was wrong").
3. **Why that observation meets (or fails) the criterion** — the inference, stated explicitly.
4. **Severity** — how bad, on a named scale, and why that level and not the one above/below.
5. **The decision**, and any **edge case / ambiguity** you had to resolve, plus which way you resolved it and on what basis.
6. **What would change your mind** — the falsifier.

Candidates are marked down for *"lacked sufficient specificity, quantitative thresholds, and/or defined acceptance criteria."* Conversely, the praised behaviour is *"mapping criteria and documenting rationale for each decision."*

### E3. "Rubric-based evaluation & guideline adherence" as an assessed skill
The competency being tested is **fidelity to a written standard under time pressure**, which decomposes into:
- **Guideline precedence** — when two rules conflict, which wins? (Reported good practice: *"clear conflict-resolution using source hierarchies."*)
- **Tie-breakers** — one candidate was explicitly told to improve *"explaining tie-breakers and decision rationales in greater detail when distinguishing between similar criteria."*
- **Adjudication** — how disagreements between raters get resolved.
- **Calibration** — how you keep yourself consistent across a long batch, and consistent with other raters (inter-rater reliability).
- **Partial credit** — *"how to score partial correctness"* was named as a gap. Most real rubrics are not binary.
- **Edge cases** — building a *"detailed edge-case test set."*
- **Not over-reaching the rubric.** One candidate's complaint is instructive in reverse: they were assessed on *QA Lead / Calibration Lead* scope for a *Generalist* JD and argued the question bank was mis-tiered. **Lesson: answer at the level the rubric asks for, and name the level you are answering at.** If asked a "design the rubric" question on a "apply the rubric" role, say explicitly: *"As the evaluator applying this rubric I would X; the rubric author's job is Y — I'd escalate that."*

### E4. How this maps onto the candidate's verified ground truth
`config/profile.md` is the only permitted source for his experience. The mapping is genuinely strong — but it must be stated in *his* real terms:

| Interview topic | Ground-truth material he may cite | Notes |
|---|---|---|
| Rubric-based evaluation & guideline adherence | **BugAgents report-promotion gate** — "scope match + HEAD match + non-empty repro + evidence files must exist"; promoted 2, **refused 34 unverified candidates**. That is literally a rubric with hard criteria and a documented false-positive/false-negative story. | Strongest single answer he owns. |
| Documentation of rationale | Optum: "generating audit-ready documentation and discrepancy reports for CMS"; "regulatory documentation, statutory compliance checks". Also AgentSwarm's independent numerical audit: **22 of 25 claims verified exact**, with all 5 defects located and disclosed. | "Audit-ready documentation" is the same artifact type as an eval rationale note. |
| Error & Edge-Case Detection | BugAgents: **8 findings, 14 CWE classes, 5 High/Critical**; the anti-fabrication guard "catches 8/8 seeded fabrications". | Cite severity counts only — **never vendor/asset/class** (profile rule 7). |
| Data quality review & QA validation | Black Piano self-healing data-quality agent (resolves missing brand domains, retries 3×, escalates for human review); Optum "zero-tolerance quality gates on high-volume transaction datasets". | Direct. |
| Judgment under ambiguity | AgentSwarm: **0 oracle violations across 1,254 tool calls**, **0 of 2 self-assessing agents overclaimed**; and the honest recording that Paper 2's DESI agreement is **circular** and its S8 result **tuned**, recommending non-submission. | The circularity disclosure *is* the ambiguity-judgement answer. Rare and strong. |
| Judging When to Step In | "Human-in-the-Loop Escalation" and "Bounded Autonomy" are listed skills; the data-quality agent "escalates via email for human review only when unresolved". | Maps exactly to the 20-min interview topic. |
| Hands-On Use of AI Tools | Multi-CLI orchestration, DeepSeek Harness, FastMCP MCP tool, multi-model A/B evaluation. | Direct. |
| Following Detailed Instructions Exactly | The anti-fabrication guard and review invariants ("0 failures; every check fires when violated"). | Direct. |
| Spreadsheet proficiency (baseline) | Profile lists **Google Apps Script**, Sheets pipelines ("auto-exported Google Sheets pipelines"), BigQuery, Looker Studio. **It does not list Excel or VBA.** | ⚠️ See risk below. |

**⚠️ Spreadsheet risk.** "Spreadsheet proficiency (baseline)" is a stated topic and profile.md lists no spreadsheet tool by name as a *skill* (Sheets appears only inside project descriptions; Apps Script is listed). He should **not** invent Excel/VBA/pivot-table depth. Honest framing: he builds and maintains spreadsheet-backed data pipelines and has automated Sheets exports; if asked for a specific Excel function he does not use, say so and describe the equivalent operation he performs in SQL/Sheets. Fabricating spreadsheet depth is exactly the failure mode the profile's anti-fabrication rules exist to prevent — and micro1's own feedback language rewards *specificity*, which he cannot fake convincingly under time pressure.

---

## F. Pay & role landscape (incl. India)

### F1. Pay structure — VERIFIED mechanics, ANECDOTAL amounts
**VERIFIED (official):** *"Payments happen on a biweekly basis through Deel… Payments are in USD, based on the number of hours you worked **or per task** (depending on your project), at the rate fixed during onboarding."*

So there are **two contract shapes**, and this matters enormously:
- **Hourly** — paid for hours worked (tracked in Hubstaff).
- **Per-task / per-deliverable** — paid *"upon task completion (as determined by Client's project leadership)"*, explicitly **not** by hours worked.

**VERIFIED (geographic exclusion list).** micro1's expert FAQ states it cannot hire residents of: Afghanistan, Belarus, China, Cuba, DR Congo, Hong Kong, Iran, Iraq, Libya, Macao, Myanmar, North Korea, Russia, Somalia, South Sudan, Sudan, Syria, Venezuela, Ukraine, Yemen, Ethiopia. **India is not on the list** — he is eligible.

**ANECDOTAL — advertised ranges observed in micro1's own official job posts (these are company-posted, so treat the *ranges* as reliable):**
| Track | Observed advertised range |
|---|---|
| AI Agent Task Evaluator | $20–$45/hr |
| AI Evaluation Analyst | $20–$30/hr |
| AI Evaluation Specialist | $22–$70/hr |
| Data Scientist | $30–$130/hr (also listed $245–$280/hr in a later week) |
| Software Developer / Backend / Frontend / Full-stack | $60–$120/hr |
| Data Engineer (core team, FT) | $140K–$180K/yr |
| Financial Data Privacy Analyst | $35–$70/hr |
| Legal Expert | $42–$55/hr; $25–$30/hr (two separate postings, same title) |
| **US Tax Law Analyst (EA/CA) — explicitly "30 India-based" hires** | **$15–$30/hr** |
| Video Data Reviewer | $10–$15/hr |
| Language experts (Hindi, Bengali, French, Swedish, Hebrew) | $10–$30/hr |

**India-specific findings:**
- **VERIFIED-adjacent:** micro1 explicitly advertised for **"30 India-based US Tax Law experts"** at **$15–$30/hr** — proof that India-based hiring is real and that the advertised rate for India-based expert roles sits at the lower end of the global bands.
- **ANECDOTAL:** a candidate thread *"Anyone from India doing software dev work on Micro1 AI?"* asks precisely whether *"they heavily slash the hourly rates because of our location"* — **4 comments, no clear answer. Unresolved.**
- **ANECDOTAL:** an India-based-adjacent poster set their rate to **$10/hr** and had never been selected, wondering whether a low self-quote was itself a negative signal. Another candidate explicitly said choosing the lowest rate was *"big mistake."* Several US candidates got in at the **$50/hr base** for a generalist/video role; one reported **$70**.
- **Practical inference (not a verified fact):** since he states his own expected rate during application and the contract is *"at the rate fixed during onboarding"*, the number he enters is consequential. Candidates on both sides report under-quoting and then being unable to raise it. **He should quote within the advertised band for the role and not reflexively bottom out.**

### F2. Documented pay risks — ANECDOTAL, but repeated and specific
These are the most decision-relevant commercial facts in this brief. All ANECDOTAL, all reported by multiple people, none contradicted by micro1 in-thread:

1. **Advertised rate ≠ contracted rate.** A Risk & Compliance Expert applied at **$45–60/hr**, then received a contract paying a *Reviewer* $45/hr but placing him as a *Trainer* at **0.667 × the hourly rate**. Another: accepted at $45/hr, contracted at **0.5 ×** for *"EVERY deliverable… regardless of how many hours I work."* Another quoted **0.375 × $20** (Trainer) and **0.125 × $20** (Reviewer). A third: **$35/hr** accepted for a role simultaneously advertised at **$50/hr** minimum.
2. **"Completion" is defined by the client.** The contract reportedly says payment is *"upon task completion (as determined by Client's project leadership)"* — with no objective completion test. A candidate reports submitting a task and receiving *"a 20-page list of revisions."*
3. **Per-task work can go unpaid for long periods.** A high-visibility post: *"Be careful accepting pay-per-task projects on micro1… the review process has since been paused indefinitely. My work is still pending, payment cycles have passed."*
4. **Screening/onboarding hours may not be paid.** One candidate completed *"the micro ai and client screeners before the client paused the project"* and asked whether the **7 hours** would be paid, with *"nothing showing in the portal."* Counter-examples exist — another was paid $150 for onboarding, and another had their 7 onboarding hours paid.
5. **Onboarding hours can be capped below actual time.** *"they cap the onboarding hours to only 7, it took me actually about 20h."*
6. **Same role, different rates.** Multiple reports of identical projects advertised at materially different rates.

**Mitigation he should apply before signing anything:** get the **rate basis (hourly vs per-task)**, the **multiplier**, the **per-task definition**, and the **review SLA** in writing before signing; ask explicitly *"what happens to completed-but-unreviewed tasks if the project pauses?"* One candidate's advice is sound: *"If there is no clear answer, do not accept the project."*

### F3. Project-work realities — ANECDOTAL
- Work availability is **bursty**; projects pause and end without notice. One candidate lost access after 27 days.
- The advertised scale of a project may exceed reality (*"The '10k' project they advertised is actually only at 1.5k on Slack"*).
- Client-side screeners **after** contracting can still end the engagement (multiple reports of offboarding after passing micro1's own assessment).
- Positive counterweight: a 6-month veteran covered rent on micro1 alone and said *"the pay is no joke."* Another reported ~40 hours/week available at more than double their local full-time rate.

---

## G. Legitimacy & safety

### G1. Is micro1 real? — VERIFIED YES
Real company, real address, real executives, real press, real contracts, real payouts reported by multiple candidates (biweekly via Deel). The *"it doesn't exist"* scam hypothesis is **false**. Two independent, named, verifiable staff respond publicly in the subreddit.

### G2. Legitimate criticisms — VERIFIED or well-corroborated
These are genuine and should not be dismissed, but they are **business-model criticisms, not fraud**:
1. **Interview data is used to train micro1's own models — VERIFIED from their own policy.** The Candidate Privacy Policy states: *"we reserve the right to use de-identified information collected from interviews, including audio, video, transcripts, and assessment results, to train and enhance our proprietary machine learning models."* It also states, explicitly: *"we do not share your data, de-identified or otherwise, with AI model companies for the purposes of training their models."* **Note the exact scope: micro1 may train its own models on it; third-party labs may not.** A candidate post dated 2026-08-31 documented that this wording changed on **2026-07-21** (policy "Last updated: July 21, 2026" — confirmed directly). The earlier framing was broader.
2. **There is an opt-out — VERIFIED.** The policy says: *"To opt-out of AI training on your information, delete your account or access a copy of your information, please check HERE"* → `talent.micro1.ai/delete-account`. Note this is **account deletion**, i.e. the opt-out and the "delete my account" action are the same button.
3. **Government ID is collected — VERIFIED.** *"If necessary to verify your identity… we may also collect government ID information and photos."* It is a required step of certification.
4. **An automated assessment is reviewed by a human before a final decision — VERIFIED.** The policy states: *"We will also use automated tools to perform an overall assessment… The overall assessment will be reviewed by a human evaluator before a final decision is made."* It also provides an **appeal route**: email `privacy@micro1.ai` to appeal a decision based on automated technologies.
5. **The official subreddit is company-moderated — VERIFIED observationally.** Critical posts get removed by `micro1_ai-ModTeam` and several candidates state criticism is suppressed. A well-upvoted "micro1 is a scam" post exists only in `r/AiTraining_Annotation` because, per its author, it was blocked in the official sub. **Practical consequence: the official subreddit is a marketing channel with a support function; read its critical content on the independent subs (`r/AiTraining_Annotation`) instead.**

### G3. Scam / phishing red flags — what to check
**VERIFIED official guidance:**
- **Official sender domains are exactly `@micro1.ai`, `@micro1.io`, `@micro1.co`.** micro1's FAQ states all three are verified. A candidate was confused by receiving the *same* shortlisting email from both `.io` and `.ai` — the official answer is that **both are legitimate**. So domain variety is *not* by itself a red flag here, but any *other* domain is.
- Official contacts: `support@micro1.ai`, `privacy@micro1.ai`, `dpo@micro1.ai`, `press@micro1.ai`.
- Official login/dashboard: `talent.micro1.ai`. Interview: `interview.micro1.ai`. Jobs: `jobs.micro1.ai`.
- **Related-domain caution:** a job board at `microonejobs.com` ("micro1 — Remote jobs for the world's best talent") appeared in search results and presents a micro1 sign-in. **It is not on micro1's own sitemap or official domain list.** Do not enter credentials there; go to `talent.micro1.ai` directly. Grade: **UNVERIFIED / treat as untrusted.**
- A third-party site, `thebudgetdiet.com/is-micro1-legit`, markets itself as *"My Honest Review (+Tips For Passing Interview!)"* — **it was not reachable from this environment and is unread.** Do not rely on it. Note that "passing the interview" content is often affiliate/referral driven — micro1 runs a **referral bounty of up to $3,000**, which is a structural incentive for third parties to publish encouraging content about micro1. **Discount all referral-adjacent "micro1 review" content accordingly.**

**Red flags that DO apply to this ecosystem:**
| Red flag | Status here |
|---|---|
| Unsolicited recruiter emails at high frequency, from rotating names | **Reported.** A candidate listed *"Sanjay, Adib, Nayla, Lucas"* sending near-identical CTAs. Micro1 does send automated + semi-automated outreach. Not proof of fraud, but it means **an email is not evidence of a real opportunity.** |
| Being offered/considered for a role never applied to | **Reported and consistent with the model.** One candidate missed an offer for a "GitHub Contributor" role they never applied to. micro1's model does proactive matching. |
| Payment demanded *from* the candidate | **No reports found.** No fee is charged to apply. Treat any request for money as fraud. |
| ID/OTP/bank details requested early | **Government ID is legitimately required — but only after passing the interview, during certification, and inside `talent.micro1.ai`.** Treat any ID/bank request arriving *before* an interview pass, or off-platform, as phishing. |
| Crypto payment / gift cards / "equipment purchase" | **No reports found.** Any such request = fraud. |
| Unpaid work demanded up front | **Partially applies.** Screeners/onboarding are sometimes paid, sometimes not, sometimes capped. This is a commercial risk to negotiate, not evidence of fraud. |

### G4. Concrete pre-commitment checklist for him
1. Verify every email sender domain ∈ {`micro1.ai`, `micro1.io`, `micro1.co`}. Anything else → don't click; log in to `talent.micro1.ai` directly.
2. **Never** enter credentials on a link from an email; navigate to `talent.micro1.ai` manually.
3. Share government ID **only** inside the official talent dashboard, **only after** passing the interview. Never over email/WhatsApp/Telegram.
4. Before signing a contract, confirm in writing: rate basis (hourly vs per-task), any **multiplier** (Trainer/Reviewer factors), the per-task definition, the review/payment SLA, and what happens to completed-unreviewed work if the project pauses.
5. Decide consciously about the **AI-training clause**: interview audio/video/transcripts/assessment results may be used to train micro1's own models. Opt-out = account deletion at `talent.micro1.ai/delete-account`. If he is uncomfortable, he can still interview (the exposure is his interview recording, not his ID) but should know it.
6. Keep the recorded interview in mind — it is **retained and available in his profile link**. Speak as if it will be reviewed by a client.
7. If rejected, **request feedback** (officially offered) and if an automated decision is involved, he may appeal to `privacy@micro1.ai`.
8. Treat micro1 as **one parallel pipeline**, never as the plan. Certification ≠ placement; HMR can run 30 days.

---

## H. Source table

| URL | Supports | Confidence |
|---|---|---|
| `micro1.ai/` | Company positioning, three products (Realm/Cortex/Robotics) | High (vendor) |
| `micro1.ai/experts` | "Take the AI interview" step; Zara named; certification→projects; official email domains; country exclusion list; certification ≠ placement | High (vendor) |
| `micro1.ai/experts/opportunities` | Roles portal exists | High (vendor) |
| `micro1.ai/experts/reviews` | Vendor-curated testimonials incl. Zara praise; claims "4.34/5, 465,974 reviews" (**implausible; vendor-claimed only — do not repeat**) | Low for numbers |
| `micro1.ai/ai-interview-guide` | **Official format**: conversational Zara interview; question types; real-time certification result; feedback option; prep steps | **High (vendor policy)** |
| `micro1.ai/interview-questions` | Official question types + published soft-skill & role examples; "no two candidates receive the same questions" | **High (vendor policy)** |
| `micro1.ai/interview-prep` | Free AI practice interviews, 18-min per role | High (vendor) |
| `micro1.ai/interview-prep/data-analyst-interview-questions` | 10 official Data Analyst sample questions; "document these choices to maintain reproducibility"; QA/documentation emphasis | **High (vendor policy)** |
| `interview.micro1.ai/mock-interview` | The actual mock-interview app (same product as the real interview) | High (vendor) |
| `micro1.ai/cortex` | Agent-evaluation work definition: rubrics, scoring, failure diagnosis, human review beyond LLM-as-judge | **High (vendor)** |
| `micro1.ai/blog/why-the-ai-evaluation-layer-is-your-real-ip` | "grade the reasoning chain", "isolate that exact trace", "failure taxonomies", "graded multi-turn traces", "continuous calibration" | High (vendor) |
| `micro1.ai/legal/privacy-notice-candidates` | **Interview data collected** (audio/video, screen share, transcripts, scores, proctoring); ID collection; AI training on interview data; no third-party-lab training; opt-out = account deletion; human review before final decision; appeal route | **High (legal)** |
| `micro1.ai/legal/privacy-policy` | Entity, HQ address, contacts, scope carve-out for candidates | **High (legal)** |
| `micro1.ai/newsroom` | Press index (TechCrunch, Forbes, CNN, WSJ, CNBC, BI, NBC, LA Times) | High (vendor-curated index) |
| `techcrunch.com/2026/08/20/ai-data-startup-micro1-reaches-500m-gross-run-rate...` | "$500M gross run rate" headline | Medium (**headline only** — article body did not extract) |
| `micro1.ai/careers` | Core-team hiring, executives, "research lab building data infrastructure" | High (vendor) |
| `micro1.ai/forum/building-your-career-with-micro1-16` | Recurring official webinar: "from the AI interview to certification and landing roles"; Director of Recruitment Marketing | High (vendor) |
| `reddit.com/r/micro1_ai` (via `red.artemislena.eu`) | Official sub, 32.3k members; staff Community Managers; status vocabulary; candidate testimony | Medium (community) |
| `r/micro1_ai` post `1t2nr9n` "New to micro1? Start here!" (staff) | **Official funnel**: Zara evaluates communication/logical reasoning/role skills; SWE→live coding, human-data→task exercises; ID certification; 30-day window; Hubstaff/Deel/Slack; **biweekly USD pay, hourly OR per task at onboarding rate** | **High (staff/official)** |
| `r/micro1_ai` post `1vu9vwm` "What I learned after failing 10 ZARA AI interviews" (138 upvotes) | Zara pace/fatigue; combined multi-part questions; single-sitting compression; silence handling | ANECDOTAL |
| `r/micro1_ai` post `1wlmcdq` "Tips for Cracking the Zara AI Interview" (119 upvotes) | Seed the intro; 2–3 min answers; numbered structure; Zara extracts follow-ups from intro | ANECDOTAL |
| `r/micro1_ai` post `1wgvs2t` "My experience with Zara" | Intro→adaptive navigation; transcribed questions; rephrase allowed; mock interview ×3; STAR; no scroll-back | ANECDOTAL |
| `r/micro1_ai` post `1x3rs4e` + staff reply | Interview vs test portion is **role-specific**; pre-interview screen states skills/duration | **Staff reply (near-official)** |
| `r/micro1_ai` post `1ufyavp` (staff megathread) | Official troubleshooting: Ethernet, no public Wi-Fi, Chrome incognito / Firefox Private; known Zara freeze/lag/repeat bugs | **High (staff)** |
| `r/micro1_ai` post `1u131ny` "Tips Please" | **Verbatim micro1 feedback email** → rubric vocabulary (severity taxonomy, inter-rater reliability, partial correctness, rationale mapping) | ANECDOTAL (single leak, high value) |
| `r/micro1_ai` post `1vzcspt` "Moving Target of Feedback" | Graded down for lacking "specificity, quantitative thresholds, acceptance criteria"; asked to **request detailed feedback** | ANECDOTAL |
| `r/micro1_ai` post `1qrde4g` | **Retake: same role after 30 days or apply to a different role immediately**; rubric-based written task; 48h feedback; 45-min webinar | ANECDOTAL |
| `r/micro1_ai` post `1w3hb4z` (staff, week of Aug 31) | **"AI Agent Task Evaluator" — $20–$45/hr**; sibling evaluator roles & rates | **High (staff post)** |
| `r/micro1_ai` post `1ta0rb0` (staff, week of May 11) | Role/pay catalogue incl. **"30 India-based" US Tax Law Analyst at $15–$30/hr** | **High (staff post)** |
| `r/micro1_ai` posts `1s1592a`, `1sujbpu`, `1u2fvaq`, `1vekzdq` | Rate multipliers (0.667/0.5/0.375/0.125), "as determined by Client's project leadership", pay-per-task review paused → unpaid | ANECDOTAL (multiple, consistent) |
| `r/micro1_ai` post `1wyjhe9` | A Data Analyst contractor: micro1 rate >2× local full-time; ~20–40 hrs/week available | ANECDOTAL |
| `r/micro1_ai` post `1x39w6e` + staff reply | "Partial interview" concept; staff explain re-interviewing = different clients/requirements | **Staff reply (near-official)** |
| `r/AiTraining_Annotation` post `1w3pvtm` | Privacy-policy change (2026-07-21) and what it did/didn't fix | ANECDOTAL + **VERIFIED against policy text** |
| `r/AiTraining_Annotation` post `1wb5x8v` "My honest experience after 6 months" (79 upvotes) | Pay is real; support is weak; activity-monitoring false flags; onboarding quality varies | ANECDOTAL |
| `r/AiTraining_Annotation` posts `1wdadc6`, `1vb399j`, `1vqpa15` | "micro1 is a scam" genre — **claims of data-harvesting and endless rejections; contradicted by the company's verified existence. Record as sentiment, not fact.** | ANECDOTAL (contested) |
| `r/AiTraining_Annotation` post `1wgi43s` | "Just got a Micro1 AI Evaluator contract" — title is real | ANECDOTAL |
| `r/AiTraining_Annotation` posts `1weywlz`, `1wjkjfl`, `1wxg5dm` | Post-contract client screeners ("Feather", "Horizon") can still offboard; 7-hr onboarding; guidelines changed mid-flight | ANECDOTAL |
| `r/micro1_ai` post `1qhbx72` + replies | Same shortlisting email from `.io` and `.ai` — both official | ANECDOTAL (consistent with vendor FAQ) |

---

## I. What remains unknown / could not confirm

1. **Glassdoor and Blind were never reached** (DNS-blocked; no search API). All employer-review data is therefore absent. This is the largest gap. If the Lead has network access from another context, Glassdoor interview reports for "micro1" would be the single best addition.
2. **Whether his 43-min and 20-min interviews include a written/task portion.** Officially "role specific" — the pre-interview screen states it. **He must read that screen before starting.**
3. **Whether either interview is proctored/screen-shared.** Policy says proctoring tools exist; candidate reports are mixed.
4. **Exact retake policy.** One anecdote (30 days for same role) vs. official silence. **Unconfirmed.**
5. **Exact per-question time limits and question counts** for his two interviews.
6. **Whether the 43-min interview is Data Analyst *for a named client* or generic certification.** The screenshot says only "micro1" and the topics are generic. Likely pool certification.
7. **Whether typing is scored differently from speaking.** Candidates speculate; **no evidence either way.** Official position is simply that both are accepted. Do not assume typing is safer.
8. **Pass rates.** No credible figure exists. The only data points are individual tallies (e.g. 12 interviews → 6 DQ, 4 not selected, 2 pending). **Do not quote a pass rate.**
9. **Actual pay rate for his two roles.** Not stated in the invitations. Advertised bands: AI Agent Task Evaluator $20–$45/hr; Data Analyst roles vary widely.
10. **India-specific rate adjustment.** An explicit candidate question on this received no definitive answer. The only hard India data point is the $15–$30/hr India-based tax-law role.
11. **The "4.34/5, 465,974 reviews" figure on micro1's reviews page is not credible** as a review count at that company size and could not be checked (Trustpilot unreachable). **Do not repeat it.**
12. **TechCrunch article body** did not extract — only the headline. The "$500M gross run rate" claim is therefore headline-grade, not article-grade.
13. **`microonejobs.com`** — presents as micro1 but is not on micro1's sitemap or official domain list. **Unverified; treat as untrusted.**
14. **`thebudgetdiet.com/is-micro1-legit`** — unreachable; unread. Excluded from all conclusions.

---

## J. Prep implications specific to this candidate (profile-anchored)

Anchored strictly to `config/profile.md`. Nothing here invents experience.

**J1. The strongest strategic insight.** micro1's assessed skills — *rubric adherence, documented rationale, severity taxonomy, edge-case detection, calibration, deciding when a human must step in* — are the exact competencies his own projects were built to enforce. He is not stretching. The risk is not capability; it is **terminology and answer shape under a timer**. He should rehearse saying *"here is the criterion I applied, here is the evidence, here is my severity call, here is what would change my mind"* — that sentence structure is the deliverable.

**J2. Per-topic answer bank (both interviews).**

*43-min Data Analyst track:*
- **Data quality review & QA validation** → Black Piano self-healing data-quality agent: detects missing brand domains, reference-table lookup with LLM fallback, writes back to dataset *and* lookup table, retries 3×, escalates to human only when unresolved. Frame as a QA pipeline with a defined escalation boundary. Add Optum "zero-tolerance quality gates on high-volume transaction datasets."
- **Judgment under ambiguity & documentation of rationale** → AgentSwarm's independent numerical audit: 22 of 25 claims verified exact, all 5 defects located in prose rather than code, verdict recorded as **B+ / not publication-grade without that audit**. Then the Paper 2 self-audit that records its own DESI agreement as **circular** and its S8 result as **tuned**, and recommends non-submission. **This is the answer.** Ambiguity handled by writing down the limitation against your own interest. Do not soften it.
- **Rubric-based evaluation & guideline adherence** → BugAgents promotion gate (scope match + HEAD match + non-empty repro + evidence files must exist). **Promoted 2, refused 34.** A hard-criteria gate with an explicit false-positive posture. Name the criteria; name the refusal count; explain the asymmetry (a false promotion costs more than a false refusal).
- **Spreadsheet proficiency (baseline)** → Sheets-backed pipelines and Apps Script automation from the blog-post MCP tool work ("auto-exported Google Sheets pipelines"). **Do not claim Excel/VBA depth.** If asked for a function he doesn't use, say so and give the SQL/Sheets equivalent.
- **Error & Edge-Case Detection** → BugAgents: 8 findings, 14 CWE classes, 5 High/Critical, 3 Medium; anti-fabrication guard catches **8/8 seeded fabrications**. **Cite severity and class counts only — never vendor, asset, or vulnerability class** (profile rule 7).

*20-min AI Agent Evaluator track:*
- **Following Detailed Instructions Exactly** → The anti-fabrication guard and the review invariants ("0 failures; every check fires when violated"). Also JobAgents' deterministic scoring path with **zero model calls** — a deliberate refusal to let judgement leak into a rule-governed path.
- **Hands-On Use of AI Tools** → Multi-CLI orchestration (omp/pi/agy/Antigravity), DeepSeek Harness, a custom **FastMCP** tool, multi-model A/B evaluation, LoRA/QLoRA fine-tuning, the BrandXY result (**76.5% vs 25.5% baseline, +51%**, GPT-OSS-20B on AMD MI300X).
- **Judging When to Step In** → "Human-in-the-Loop Escalation" and "Bounded Autonomy" are listed skills; the data-quality agent escalates by email only when unresolved; BugAgents aborts on any out-of-scope host or offensive tool (**a live run was aborted exactly this way**). Frame as: *automate to a defined boundary, then hand over with a written reason.*
- **"Custom questions defined for the job"** → micro1's guide says he may *"create customized questions in advance to better showcase your expertise."* **He should prepare 2–3 of these deliberately**, aimed at agent-trace grading and rubric design.

**J3. Delivery mechanics to rehearse (from §B/§C).**
- Never silent. *"Let me think about that for a moment"* — then structure out loud.
- Numbered structure; ~2–3 minutes per answer.
- Seed the intro with the topic he wants drilled (agent evaluation + audit), because Zara builds follow-ups from the end of the intro.
- Ask for rephrasing immediately on any miss — there is no scroll-back.
- Read the pre-interview screen for skills assessed, duration, and whether a test portion is included.
- Run the official mock interview **2–3 times** on `interview.micro1.ai/mock-interview` before the real thing.
- Use Firefox (or Chrome incognito) if Zara hangs; wired connection; no refresh.

**J4. Honesty guardrails (profile rules 1–13 still bind).**
- No invented metrics, employers, titles, or skills — micro1's feedback language rewards *specificity*, which is precisely what fabrication cannot sustain under follow-up questioning.
- Paper 1 is a **Zenodo preprint**, not peer-reviewed. Paper 2 is a **manuscript, not submitted**. The AgentSwarm verdict is **B+ / not publication-grade without a numerical audit** — state it if the work comes up.
- BugAgents findings are **submission-ready drafts**; no bounty awarded, nothing disclosed. Severity/class counts only.
- All three projects are **independent/self-directed**, not Black Piano or Pi Software deliverables. No production users, revenue, or adoption.
- Titles held: **Data Analyst** (Black Piano, Pi Software); **Enrollment Quality & Audit Representative (CMS Auditor)** (Optum). No AI/agentic title was held.
- **Note the profile's own positioning risk:** the 20-min track is titled "AI Agent Evaluator". If micro1's certification assigns that label, it is *micro1's certification label*, not a job title he has held. Do not let it migrate onto a résumé as employment.

---

*End of brief. All ANECDOTAL material in §C, §D3, §E1, §F and §G2–G3 is candidate testimony or single-source leakage and must not be represented to the candidate as micro1 policy.*
