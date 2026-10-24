# Interview Script — Wellfound AI Interview

> **How to use this.** The AI interviewer asks behavioural and technical questions.
> Each answer is ~30 seconds spoken. The **bolded phrase** is the one technical term
> worth landing; the plain sentence after it is your explanation.
>
> **Every number here traces to `config/profile.md`.** Nothing is invented.

---

## Q1. "Tell me about yourself."

I'm an AI systems engineer based in Hyderabad. For the last two years I've been building
**autonomous agent systems** — that's software where AI agents work on their own over long
periods, not just answering one question. I've shipped three of them, all live and public.
Before that I spent three and a half years in data engineering, and eleven years before that
in pharmaceutical quality auditing, which is where I learned to verify everything rather than
trust it.

**Why this works:** frames your unusual background as a *reason* for your strength rather than
something to apologise for. Lead with the 2 years of AI, not the 11 years of pharma.

---

## Q2. "Walk me through a project you're proud of."

BugAgents. Two AI agents hunting real security bugs in live bug bounty programs. The
interesting part isn't that they found bugs — it's that I built a **verification gate**, a
checkpoint every finding has to pass before it counts. It checks four things: is the target in
scope, does the code version match, is there a working proof of concept, and do the evidence
files actually exist. That gate rejected 34 findings the agents were confident about but
couldn't prove. Three passed. Two were rated High severity, CVSS 9.3 and 8.6.

**Why this works:** "34 rejected, 3 passed" is the whole story. It shows you don't trust AI
output. Avoid saying "the agents found bugs"; say the gate *proved* three.

---

## Q3. "How do you make sure an AI agent isn't making things up?"

Three layers. First, **guardrails as code** — not instructions in a prompt, but actual code
that blocks bad output. In my job pipeline, every claim in a generated resume is checked
against a facts file; if a number isn't in that file, the resume is rejected and never saved.
I tested it with 8 deliberately fake claims and it caught all 8. Second, an **independent
verifier** — a separate checker that isn't the agent grading its own work. Third, an **audit
ledger** — I use hash-chained logs, meaning each entry contains a fingerprint of the previous
one, so if anyone edits history the chain breaks. I ran 32 agent sessions and all 32 chains
verified intact.

**Why this works:** your strongest technical answer. "The audited cannot edit the audit" is
memorable. Say the layers slowly — three is easy to follow.

---

## Q4. "Describe a technical challenge and how you solved it."

When I ran multiple AI agents in parallel, they'd sometimes report success on work that had
failed. The problem was that the agents were checking their own work. So I moved the checking
outside them — a separate **oracle**, an independent program that verifies each agent's output
against the actual files and numbers, not against what the agent claimed. That caught
something important: across 1,254 tool calls there were zero violations, and two agents that
self-assessed their own performance scored themselves exactly what they'd independently
earned — no overclaiming.

**Why this works:** a real engineering story with a diagnosis and a fix, not a buzzword list.

---

## Q5. "How do you handle working with messy data?"

At Black Piano I built a **self-healing pipeline** — a data pipeline that fixes its own
problems. The issue was missing company domains, which broke the logos on client dashboards.
So the system checks a reference table first, falls back to an LLM to look it up if it's
missing, writes the answer back to both the dataset and the lookup table, retries three times
on failure, and only emails a human if it still can't resolve it. That's eighteen ETL
pipelines feeding dashboards for four enterprise clients. The principle is: automate the fix,
escalate only the genuinely unknown.

**Why this works:** "automate the fix, escalate the unknown" is a crisp principle.
Interviewers remember principles.

---

## Q6. "What's your experience with LLMs and model training?"

I've done **LoRA and QLoRA fine-tuning** — that's a way of adapting a large model cheaply, by
training a small number of extra parameters instead of the whole model. I fine-tuned
GPT-OSS-20B on AMD MI300X hardware for a brand-safety task and got 76.5% accuracy against a
25.5% baseline. I also run **model evaluation** — comparing models on the same task to see
which is actually better, including measuring bias. I benchmarked six different coding agents
over two rounds.

**Why this works:** honest about scope — you've done fine-tuning and evaluation, not
pre-training. Don't claim more.

---

## Q7. "Tell me about a time you failed."

My first agent pipeline generated resumes that credited my side projects to my employer.
That's a factual error, and it would have gone out to real companies. The fix wasn't better
prompting — I'd already told the model not to do it and it still did. So I wrote
**deterministic validation**: code that walks the resume structure and rejects any independent
project appearing under an employer section. The lesson is that if a rule matters, it has to
be enforced in code, not requested in a prompt.

**Why this works:** the single best answer in the script. A genuine failure, a structural
lesson, and "enforce in code, not in prompts" is a mature insight.

---

## Q8. "Why this company / why this role?"

[Adapt per company.] What draws me is that the hard part here isn't making the AI work once —
it's making it reliable across many cases. That's the problem I've spent two years on:
verification, guardrails, and making agents trustworthy rather than just impressive. I'd
rather work on the reliability layer than on demos.

---

## Q9. "Do you have any questions for us?"

Ask two of these — they signal seniority:

1. "How do you currently decide whether an AI feature is good enough to ship?"
2. "Where does verification sit in your team — is it one person's job, or built into the
   pipeline?"
3. "What does the first 90 days look like, and what would make you say this hire worked?"

---

## Delivery notes

**Timing.** The whole script is ~8 minutes of speech across 9 answers. You have 15 minutes, so
you have room to breathe. Don't rush.

**Say numbers slowly.** "One thousand two hundred and fifty-four tool calls" lands; a mumbled
figure doesn't. Slow down for every number.

**Pause before answering.** A one-second pause reads as thoughtful, not slow. The AI
interviewer won't penalise it.

**Two things to avoid.**

- **Don't say "we"** for your solo projects. They're yours — say "I built."
- **Don't inflate seniority.** Never say "led a team" or "staff-level." Your profile is
  explicit about this, and interviewers probe titles. Your real record is strong enough
  without it.

**On the BugAgents disclosure rule.** Keep saying "two High severity, CVSS 9.3 and 8.6" and
nothing more. Do **not** name the vendor, the product, or the vulnerability type — those
reports aren't submitted yet. If they push for detail, say: *"I'm keeping specifics private
until the disclosure process completes, but I'm happy to walk through the verification gate
that validated them."* That answer itself demonstrates good security judgement.

---

## Quick reference card

| Question | Land this |
|---|---|
| Tell me about yourself | 2 yrs agents · 3 live systems · 11 yrs QA discipline |
| Proud project | BugAgents · gate rejected 34, passed 3 · CVSS 9.3 / 8.6 |
| Prevent hallucination | Guardrails as code · independent verifier · hash-chained ledger |
| Technical challenge | Moved verification outside the agent · 1,254 calls, 0 violations |
| Messy data | Self-healing pipeline · 18 ETL pipelines · automate fix, escalate unknown |
| LLM / training | LoRA/QLoRA on MI300X · 76.5% vs 25.5% baseline |
| A failure | Projects credited to employer → deterministic validation in code |
| Why us | Reliability layer, not demos |
| Your questions | "How do you decide a feature is good enough to ship?" |

**Numbers you may cite (all verified):** 32 agent runs · 32/32 hash chains intact · 1,254 tool
calls, 0 oracle violations · 34 findings rejected, 3 promoted · CVSS 9.3 and 8.6 · 18 ETL
pipelines · 76.5% vs 25.5% baseline · 8/8 seeded fabrications caught · 1,441 autonomous turns ·
330 turns through an API blackout.
