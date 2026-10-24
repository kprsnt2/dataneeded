# HR Round — The "Trial" Question, AI Disclosure, and Documents

**Context:** technical round done. Next is **HR**, and they have asked for **prior promotion letter, payslips and other documents**.

---

## §0 — The 60-second read

1. **Yes — ask about the trial framing. Directly, and in writing.** *"It might work or not"* is a material fact about your job security, and you are entitled to ask what happens to **you** if the project doesn't land. Asking this is a sign of seniority, not doubt. §1.
2. **The risk is specific and worth naming:** on a project that may not survive, the person who owns the experiment is the first cost to cut. Get the **department of record** and the **fallback** clarified. §1.3.
3. **Do not volunteer that you used AI to build. Do not hide it either.** It is a non-issue presented as a confession, and a real issue if you dodge it. §2.
4. **The distinction that matters is tool use versus competence** — and the honest version of your answer is stronger than either the confession or the silence. §2.2.
5. **Do not send documents until the offer terms are clear.** Payslips are normal at offer stage in India. They are also leverage you only get to spend once. §3.

---

## §1 — The "trial and error" question

### 1.1 What they actually told you

*"It's a trial and error — new team, new experiment, and you will have a lot of challenges. It might work or not. Not sure, as it's the first time implementing."*

**Three things are being communicated at once, and only one of them is a warning:**

| What it sounds like | What it also is |
|---|---|
| "This might fail" | **Honest disclosure** — better than a company that pretends certainty. Credit them for it. |
| "New team, new experiment" | **Greenfield ownership.** Your first-90-days plan is the job. |
| "You will have a lot of challenges" | **A soft expectation-setter** — usually a precursor to "so the package is what it is." |

**The subtext to be alert to:** *"it might not work"* is often said before an offer precisely to lower expectations on comp and to pre-justify a demanding first year. That does not make it dishonest — but you should notice it and price it.

### 1.2 Yes, ask. Here is how, without sounding like you're doubting them

The wrong question is *"what if it fails?"* — it sounds like fear. The right question is about **structure**, and it is the same question a good product owner would ask about any project:

> *"I appreciate you being straight about it being an experiment — I'd rather know that than be sold certainty. Can I ask what the structure looks like if it doesn't land as planned? Specifically: which team and department would I sit in on paper, and if the programme is paused, is there a path into an existing function, or would the role end with it?"*

**Why this lands well:** it shows you plan for failure modes, which is exactly the instinct the role requires — the same instinct as *"if that fails, I step in."* You are not asking for a guarantee. You are asking to understand the shape of the risk.

### 1.3 The four things to get clarified

| # | Question | Why it matters |
|---|---|---|
| 1 | **"Which department am I hired into — Health & Analytics, or a separate innovation/experimental unit?"** | A role inside a core function survives a failed experiment. A role inside a temporary unit does not. |
| 2 | **"If the programme is paused or wound down, what happens to the position?"** | The direct version of the question. Ask it plainly; a vague answer is itself information. |
| 3 | **"Who is the sponsor, and what's the funding horizon?"** | A sponsored project with a budget cycle is real. An unfunded mandate dies at the first review. |
| 4 | **"What does success look like at 6 months, and who decides?"** | If nobody can name the success criteria, the project has no definition of done — and you would be the one held to an undefined bar. |

**Get the answers by email if you can.** *"Could you confirm the reporting line and department in writing?"* is a completely normal request before signing, and it protects you later.

### 1.4 The asymmetry you should be aware of

You are leaving **13 LPA, remote, in your own house**. They are offering **~22 LPA, Mumbai, office-based, on a project that may not survive**.

- If the project succeeds, you gain a genuine AI role and a large salary jump.
- If it fails, you have **relocated, taken on rent, and lost the job** — and the market for "product owner on a cancelled pilot" is worse than the market for your current skills.

**That asymmetry is the strongest argument you have for asking for relocation support and a joining bonus.** Not greed — risk pricing. Say it that way:

> *"I'm being asked to relocate for an experiment that may not continue. That's a real risk on my side, and it's the main reason I keep coming back to relocation support — it's the one part of the package that de-risks the move itself."*

That is a completely reasonable thing to say out loud, and a company that genuinely wants you will not be offended by it.

---

## §2 — Should you tell them you built everything with AI?

### 2.1 The short answer

**Do not volunteer it. Do not hide it. Answer it honestly if asked — and answer it in terms of outcomes, not tools.**

Here is why the middle path is right, and why both extremes are worse:

| Approach | What happens |
|---|---|
| **Volunteer it as a confession** | *"I should tell you, I used AI to build all of this."* You have turned a non-issue into a doubt. It signals that you think it is a problem — and if you think so, they will too. |
| **Hide it / deny it** | If it surfaces later — and in a role that will *require* you to use these tools daily, it will — you look evasive about something that never needed hiding. |
| **Answer plainly when relevant** | *"Yes — I use AI tooling heavily, the same way I'd use an IDE or a debugger. Here's what I own that the tooling doesn't."* Non-defensive, accurate, and it moves the conversation to the part that matters. |

### 2.2 The distinction that decides this — tool use versus competence

**Nobody in 2026 is surprised that a developer uses AI.** Your own interview was for a role that will have you doing exactly that. Asking *"did you use AI?"* is like asking *"did you use Stack Overflow?"*

**The real question behind the question is this:** *if the AI is wrong, or unavailable, or produces something you don't understand — what then?*

That is the question you should be prepared for, and it is a question you have a genuinely good answer to.

### 2.3 Your honest answer, in three parts

**Part 1 — own the usage, without apology:**

> *"Yes, heavily. I use Claude, Antigravity, DeepSeek and others as development tooling — the same way I'd use an IDE. It's how I shipped six projects while working full time."*

**Part 2 — be precise about your actual level. This is the part you must not fudge:**

> *"I can read and reason about Python and I understand the architecture of what I've built — the pipeline design, the data model, the control flow, the failure modes. Where I'm weaker is writing large amounts of code from scratch without assistance, and debugging something unfamiliar quickly. I'd rather tell you that than have you find out in week two."*

**Part 3 — turn it into the thing they actually need:**

> *"The part I'd point at is that I know where these tools fail, because I've had to build the checks around them. My own pipeline has a guard that validates generated output against a ground-truth file before anything is written to disk, because a model violated an explicit rule while producing fluent output. That's the skill this role needs — not typing code faster, but knowing what to trust and what to verify."*

**Why part 3 is the strongest thing you have:** the job is *automating claims decisions with AI, safely*. Someone who has already built verification layers around unreliable models is more useful than someone who writes beautiful code and trusts it. **You are selling the exact instinct they need.**

### 2.4 What not to say

- **"I can understand Python but I need help with AI."** This is the sentence you drafted, and it is the wrong one — it pairs a weakness with a dependency, and it makes you sound like you would need supervision. Say *"I'm stronger on architecture and verification than on writing code unaided"* instead. Same truth, accurate framing.
- **"AI wrote everything, I just directed it."** Even if it feels honest, it understates you. You made the design decisions, defined the failure modes, and built the verification. That is the work.
- **Any claim to a level you don't have.** If you say you are a strong Python engineer and you are not, the technical round will find it. §2.5.

### 2.5 The real risk — and it is worth thinking about honestly

**This is a technical role on an AI project.** If the day-to-day is writing and debugging agent code, and you need substantial assistance for that, the gap will become visible within weeks — and a failed experiment is exactly the environment where a performance gap gets attributed to the hire.

**So the useful question is not "should I disclose?" but "is this role the right fit?"**

Two possibilities:

- **If the role is genuinely product-owner-flavoured** — defining requirements, designing the decision logic, specifying acceptance criteria, working with a separate engineering team — then your level is fine, and your domain-plus-verification profile is the point.
- **If it is hands-on agent engineering with you as the primary coder**, then you should either negotiate for support (a team around you, or a defined ramp) or think hard about whether the fit is real.

**Ask them directly in HR:** *"Is there an engineering team building this, or would I be doing the hands-on development myself?"* The answer tells you which of these you are walking into — and it is a completely legitimate question at this stage.

---

## §3 — The documents they asked for

### 3.1 What is normal, and what is not

| Document | Normal at this stage? |
|---|---|
| **Payslips (last 3 months)** | **Yes** — standard in India for offer-stage background and band verification. |
| **Promotion letter / increment letter** | **Yes** — commonly used to verify your stated history. |
| **Offer letter from current employer** | Yes, sometimes. |
| **PAN / Aadhaar / bank details** | **Only after an offer is in writing and you accept.** |
| **Relieving letters from previous employers** | At joining, not before. |
| **References** | Normal, and you should be asked first. |

**Nothing here is a red flag on its own.** Indian insurers routinely verify compensation and tenure before issuing an offer.

### 3.2 But sequence it — this is leverage you only spend once

**Ask for the offer terms before or alongside the documents.** A short, polite message:

```
Happy to share the documents. Before I do, could you confirm the terms so I can
review everything together:

- The band and grade, and the fixed/variable split
- Relocation support and joining bonus
- The department and reporting line
- Whether the offer is contingent on anything beyond standard verification

Once I have that I'll send the payslips and promotion letter straight away.
```

**Why this is reasonable rather than difficult:** payslips exist to *verify a number*. If there is no number on the table yet, there is nothing to verify. Any competent HR team understands this and will simply send the terms.

### 3.3 One caution

**Your payslips will show 13 LPA.** Once they see it, the conversation is anchored there, and the "69% jump" framing becomes *their* argument rather than yours.

**This is exactly why you should settle the number first.** You have already made the right argument — that 13 with no rent is not comparable to 22 with Mumbai rent. Make sure that argument lands **before** the payslip arrives and the conversation becomes purely about a multiplier.

**If they have already seen it, it is not fatal** — but your position becomes *"22 is generous on paper but I'm taking on rent for the first time"* rather than *"here is why the role is worth 25."* Slightly weaker, still workable. Do not panic either way.

### 3.4 Do not send

- Bank account details, cancelled cheques, or a signed offer acceptance before terms are agreed
- Aadhaar or PAN scans over WhatsApp or a personal email
- Anything to a domain that is not the company's own — verify the email domain before you attach a payslip

---

## §4 — Your questions for HR, in order

1. **"What's the band, grade, and the fixed/variable split?"**
2. **"What does relocation support and joining bonus look like?"**
3. **"Which department and reporting line am I hired into?"** — core function or experimental unit.
4. **"If the programme is paused, what happens to the position?"**
5. **"Is there an engineering team building this, or would I be the hands-on developer?"** — determines whether the fit is real.
6. **"What does success look like at six months, and who decides?"**
7. **"What's the notice period expectation, and the joining date?"**
8. **"Is the offer contingent on anything beyond standard document verification?"**

**Get the answers in writing where you can.** A verbal promise about relocation or a review cycle is worth nothing in six months.

---

## §5 — Pocket card

**On the trial framing — say this:**

> *"I appreciate you being straight about it being an experiment. Can I ask what the structure looks like if it doesn't land — which department I'd sit in, and whether there's a path into an existing function? I'm not asking for a guarantee, I'm asking so I understand the risk I'm taking by relocating."*

**On AI usage — if it comes up:**

> *"Yes, heavily — Claude, Antigravity, DeepSeek, the same way I'd use an IDE. I can read and reason about Python and I understand the architecture of what I've built; where I'm weaker is writing large amounts of code unaided. The part I'd point at is that I know where these tools fail, because I've built the verification layers around them — my pipeline validates generated output against ground truth before it's written to disk. That's what this role needs."*

**On documents:**

> *"Happy to share them. Could you confirm the band, grade, relocation support and reporting line first, so I can review everything together?"*

**Never say:**
- *"I can understand Python but I need help with AI."* — pairs a weakness with a dependency. Reframe as architecture-strong, code-unaided-weaker.
- Any claim about your Python level you cannot demonstrate.
- *"Whatever the package is, I'm fine."* — you have not agreed to 22.
- Anything to a recruiter before confirming the email domain is the company's own.
