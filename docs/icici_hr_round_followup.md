# HR Round — The Tooling Question, the Trial Framing, and Documents

**Status:** technical round done (with the **Project Manager**). Next: **HR**.

---

## §0 — The 60-second read

1. **The claims point is closed.** You already said upfront that you don't come from claims and explained the enrollment background. That was the right move and there is nothing left to follow up. §1.
2. **Your real question is about the AI tooling — and it's about timing, not honesty.** Do not raise it in HR. §2 explains why, and gives you the answer to have ready if it comes up.
3. **The PM ran your resume through an AI and asked the generated questions.** Notice what that means: **they already work this way.** Asking about tooling is not a strange request in that room. §4.
4. **Ask about AI tooling — yes.** Frame it capability-first and delivery-focused, not brand-first and personal. §4.2.
5. **Your HR question list has a wrong item and a missing one.** "Relocation bonus" is the wrong ask; **role permanence and department of record** are the right ones. §5.
6. **Keep a trigger sheet open for every call.** You've now forgotten something in two consecutive interviews — that's a pattern with a cheap fix. §6.

---

## §1 — The claims point: already handled

You said upfront that you do **not** come from a claims background, and explained the enrollment work — the application and eligibility stage, governed by CMS.

**That was exactly the right thing to do, and it is done.**

- You didn't hide it, so there is no gap to close.
- You volunteered the limitation before they probed it — the behaviour that builds credibility.
- The interviewer had your resume in front of them and chose to continue. That answers whether it was a problem.

**No follow-up needed. Do not reopen it in HR.** If it comes up again, the one-line version in §7 is already proven to work.

---

## §2 — The tooling question: should you tell them you built everything with AI?

This is your actual question. The answer is about **timing and audience**, not about honesty.

### 2.1 Disclosure is a technical conversation, not an HR one

The technical round is **over**. In it, *"how did you build this?"* is a natural question that belongs. In an **HR round** it is out of place, and here's why that matters:

| If you raise it in HR | Result |
|---|---|
| HR cannot evaluate tooling practice | They cannot credit you for it |
| It arrives with no context | It reads as *"I have a disclosure to make"* — which implies you think it's a problem |
| Wrong room, no upside | A technical fact raised to a non-technical audience |

**So: do not raise it in HR.** Not because you're hiding it — because it belongs in a technical conversation, and the technical conversation has already happened.

### 2.2 Not volunteering is not hiding

- **Hiding** = denying it if asked, or avoiding the word "AI." Don't.
- **Not volunteering** = choosing the right audience for a technical fact. That's what this is.

**The rule:**
- **Asked directly — anywhere, including HR — answer honestly and without flinching.** §2.3.
- **Not asked — don't raise it.** It isn't a confession; there's nothing to confess.

### 2.3 The answer to have ready — this is what actually matters

**Part 1 — own it, no apology:**

> *"Yes, heavily — Claude Code, Antigravity, DeepSeek. I treat them as development tooling, the same way I'd use an IDE or a debugger. It's how I shipped six projects while working full time."*

**Part 2 — be precise about what you own versus what the tool produced. Do not fudge this:**

> *"What I own is the design and the decisions: what the pipeline should do, where the failure modes are, what the controls need to be, and why. Where I'm weaker is writing large amounts of code from scratch unaided, and debugging unfamiliar code quickly. I'd rather tell you that than have you find out in week two."*

**Part 3 — land the thing they actually need:**

> *"The part I'd point at is that I know where these tools fail, because I've had to build the checks around them. My own pipeline validates generated output against a ground-truth file before anything is written to disk, because a model violated an explicit rule while producing fluent output. That's the skill this role needs — not typing code faster, but knowing what to trust and what to verify."*

**Why part 3 carries the answer:** the job is **automating claims decisions with AI, safely**. Someone who has already built verification layers around unreliable models is more useful than someone who writes clean code and trusts it. You're not defending a shortcut — you're describing the competence the role requires.

### 2.4 What not to say

- **"I can understand Python but I need help with AI."** Pairs a weakness with a dependency. Say *"architecture-strong, code-unaided-weaker"* instead — same truth, accurate framing.
- **"AI wrote everything, I just directed it."** Understates you. You made the design decisions, defined the failure modes, built the verification. That is the work.
- **Any Python level you cannot demonstrate.** If the role is hands-on and you claim senior engineering, it surfaces in weeks.

### 2.5 The honest risk — worth thinking about once, calmly

This is a **technical role on an AI project**. If the day-to-day is writing and debugging agent code unaided and you need substantial assistance, the gap becomes visible quickly — and a failing experiment is exactly where a gap gets attributed to the hire.

**So the useful question isn't "should I disclose?" but "is this the right role?"** Ask HR: *"Is there an engineering team building this, or would I be the hands-on developer?"*

- **PO-flavoured** — requirements, decision logic, acceptance criteria, working with a separate engineering team → your level is fine, and your domain-plus-verification profile is the point.
- **You as primary coder** → negotiate support (a team around you, or a defined ramp), or think hard about the fit.

**Notice the symmetry:** *"AI built my projects"* and *"if the pipeline fails, I step in"* are the same story about you. You direct and verify; you don't hand-write everything. That is a legitimate way to work in 2026 — **it just has to match the role you're accepting.**

---

## §3 — The "trial and error" framing

*"It's a trial and error — new team, new experiment, and you will have a lot of challenges. It might work or not. Not sure, as it's the first time implementing."*

### 3.1 What's being communicated

| What it sounds like | What it also is |
|---|---|
| "This might fail" | **Honest disclosure** — better than a company pretending certainty. |
| "New team, new experiment" | **Greenfield ownership.** Your first-90-days plan is the job. |
| "You will have a lot of challenges" | **A soft expectation-setter** — usually a precursor to "so the package is what it is." |

**The subtext to notice:** *"it might not work"* is often said before an offer to lower comp expectations and pre-justify a demanding first year. Not dishonest — but price it.

### 3.2 Ask about it — but ask about structure, not "what if it fails"

> *"I appreciate you being straight about it being an experiment — I'd rather know that than be sold certainty. Can I ask what the structure looks like if it doesn't land as planned? Which department would I sit in on paper, and if the programme is paused, is there a path into an existing function, or would the role end with it?"*

**Why this lands:** it shows you plan for failure modes — the same instinct as *"if that fails, I step in."* You're not asking for a guarantee, you're asking to understand the risk.

### 3.3 The asymmetry that justifies your ask

You're leaving **13 LPA, remote, in your own house**. They're offering **~22 LPA, Mumbai, office-based, on a project that may not survive**.

- Success → a genuine AI role and a large salary jump.
- Failure → you've **relocated, taken on rent, and lost the job**.

**That asymmetry is your strongest argument for relocation support and a joining bonus.** Not greed — risk pricing:

> *"I'm being asked to relocate for an experiment that may not continue. That's a real risk on my side, and it's the main reason I keep coming back to relocation support — it's the one part of the package that de-risks the move itself."*

---

## §4 — Asking for AI tooling

### 4.1 Yes, ask. The room already works that way

Your interviewer ran your resume through an AI. **You're not introducing a novel idea — you're asking to work the way they already work.** Low-risk, reasonable, and a good sign about you: candidates who ask for the tools that make them fast are thinking about output.

### 4.2 Frame it capability-first, not brand-first

**Avoid:**

> *"I would love to have Claude Code or Antigravity with Claude, as these work very well for development."*

Nothing wrong with it, but it's a preference, and preferences are easy to decline.

**Use:**

> *"One practical question — what AI tooling is available on the team? I do a lot of my work with coding assistants and they materially change how fast I can turn requirements into something working. If the team already has licences, great. If not, I'd like to understand what's approved, because it directly affects how quickly I can deliver in the first few months."*

**Why this is better:** it ties the request to **their** outcome (delivery speed), asks what exists before asking for something new, and puts tooling in the same category as any work resource — which is how a serious engineering team thinks about it.

**Then name your preference once, briefly:**

> *"I've had the best results with Claude-based assistants — I use Antigravity and Claude Code. But I'd adapt to whatever the team standardises on."*

### 4.3 Three cautions

1. **Don't make it a condition of accepting.** A request, not a dealbreaker.
2. **Expect a security answer, and be ready for it.** An insurer will have opinions about code going to external providers: *"Understood — is there an approved path, or an internal deployment? I'd want to work within whatever the security policy is."* **That answer makes you look better than the request does**, because it shows you know the constraint exists.
3. **Don't lead with it.** Role, permanence and comp first. Tooling is a detail; the role's survival isn't.

---

## §5 — Your HR question list, corrected

| Your item | Verdict |
|---|---|
| **"How many members?"** | **Good** — team size tells you whether you're the first hire or joining a function. |
| **"Is the role permanent?"** | **Your most important question.** Ask it better: *"Is this a permanent position on the company payroll, and is the programme funded beyond the initial phase?"* |
| **"Relocation bonus?"** | **Wrong ask.** Ask for **relocation support** — a defined amount, or company-arranged accommodation for the first 1–3 months. "Bonus" sounds like a windfall; "support" is a policy. |
| **"Who do I report to?"** | **Good** — follow with *"and which department am I on the payroll of?"* Core function versus experimental unit is the distinction that matters. |

**Add two:**

- **"If the programme is paused, what happens to the position?"**
- **"What does success look like at six months, and who decides?"** — if nobody can answer, there's no definition of done.

**Order:**

1. Band, grade, fixed/variable split
2. Is the role permanent, and is the programme funded beyond phase one
3. Which department and reporting line
4. What happens to the position if the programme is paused
5. Relocation support
6. Team size, and whether there's an engineering team
7. Success criteria at six months
8. AI tooling

**Comp first, then security, then details.** Don't bury the permanence question at the end — if the answer is bad, you want the rest of the call to reflect that you know it.

---

## §6 — The trigger sheet

You've forgotten something in two consecutive interviews. That's a pattern, not bad luck — and it isn't that you don't know these things. A live conversation consumes working memory, and under mild pressure the retrieval order goes wrong. **A written trigger removes the retrieval step entirely.**

Keep this open on every call:

```
MUST SAY (in any round):
1. M. Pharmacy — clears the medical-discipline requirement
2. Optum: Claims Associate (2014-16) → CMS enrollment audit (to 2023)
3. 18 ETL pipelines → BigQuery → Looker Studio (Black Piano)
4. BugAgents gate: 4 criteria, 2 promoted / 34 refused
5. rAsh Score: 300 brands, 20 cohorts, 4 models, live
6. Self-hosting answer: tier the data, don't replace the API
```

Second monitor, phone, or printed page. Nobody minds a candidate glancing at notes.

---

## §7 — Pocket card

**On tooling, if it comes up (any round):**

> *"Yes, heavily — Claude Code, Antigravity, DeepSeek. I treat them as development tooling, the same way I'd use an IDE. What I own is the design and the decisions — the pipeline, the failure modes, the controls. Where I'm weaker is writing large amounts of code unaided. And the part I'd point at is that I know where these tools fail, because I've built the verification around them: my pipeline validates generated output against ground truth before it's written to disk."*

**On enrollment, if it comes up again:**

> *"I started as a Claims Associate, then moved into enrollment audit — the application and eligibility stage, governed by CMS rules. Not claims adjudication, and I'd say that plainly. What transfers is the discipline: nine years of having to defend a decision after the fact."*

**On the trial framing:**

> *"I appreciate you being straight about it being an experiment. What does the structure look like if it doesn't land — which department I'd sit in, and whether there's a path into an existing function?"*

**On tooling availability — ask it last:**

> *"What AI tooling is available on the team? I work with coding assistants and they materially change how fast I can turn requirements into something working. I've had the best results with Claude-based ones, but I'd adapt to whatever the team standardises on — and I'd want to work within your security policy either way."*

**On permanence:**

> *"Is this a permanent position on the company payroll, and is the programme funded beyond the initial phase? And if it's paused, what happens to the role?"*

**On documents:**

> *"Happy to share them. Could you confirm the band, grade, relocation support and reporting line first, so I can review everything together?"*

**Never say:**
- *"I can understand Python but I need help with AI."* — pairs a weakness with a dependency.
- *"AI wrote everything, I just directed it."* — understates what you actually own.
- *"Relocation bonus"* — ask for relocation **support**.
- *"I'd love Claude Code or Antigravity"* with no reason attached.
- That tooling is a condition of joining.
- Anything about your Python level you cannot demonstrate.
- **Anything about AI tooling in the HR round unless asked.**
