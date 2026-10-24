# Senior Resume — Interview Guide 5 of 6: The APPROACH Section

**Covers:** the four principles in the APPROACH block — word by word.

> **Why this section matters most.** No other resume variant has it. It is the section that turns a list of projects into a **position** — and at senior level, the interview is not "what did you build" but "how do you think". Every principle here is evidenced by a system on the same page, which is what makes it credible rather than decorative.

---

## §1 — Principle 1: "Verification before autonomy"

> *"Every system above has a component that decides whether to believe the output. On a regulated decision that is not a feature, it is the design: automated approvals are tractable, automated denials are a regulatory event, and the explanation has to come from the recorded decision trace rather than a model narrating a decision it did not make."*

**This is the strongest paragraph on the resume. Break it into three separate claims and be able to defend each.**

### Claim 1 — Every system has a verification component

**Say it as an inventory, not a boast:**

> *"Every project I've built has one. In BugAgents it's a promotion gate with four conditions that must all hold — it refused thirty-four candidates to promote two. In JobAgents it's a guard that validates generated text against a ground-truth file before anything reaches disk, catching eight of eight seeded fabrications. In AgentSwarm it's a hash-chained ledger outside the agents' writable directory, so the audited can't edit the audit. In the data-quality agent it's a deterministic lookup before any model is called. Same instinct, five implementations."*

### Claim 2 — On a regulated decision it is the design, not a feature

**This is the sentence to slow down on.** It is a position, and it is the one that maps onto insurance, banking and healthcare roles.

> *"In an unregulated setting, verification is a quality feature — nice to have, and you can ship without it. In a regulated setting it's structural. If you can't show an auditor why a decision was made, the decision doesn't exist as far as the process is concerned. So the verification layer isn't something you add after the model works; it's the thing that determines whether the model is allowed to decide at all."*

### Claim 3 — The asymmetry: approvals are tractable, denials are not

**This is your single best substantive answer in any interview.** Have it ready verbatim in shape.

> *"Auto-approval and auto-decline are not the same problem, and treating them as one is the mistake I'd expect an automation programme to make.*
>
> *Auto-approval is tractable. Approving a clean, low-value, in-network, pre-authorised claim within policy limits is a bounded decision. If the system is wrong you have paid a claim you might have questioned — a cost you can measure, reserve for, and tune the threshold on. That's where the volume is.*
>
> *Auto-decline is a different risk class. A wrong denial isn't a cost line — it's a regulatory event, a grievance, possibly an ombudsman case, and a reputational one. And in Indian health insurance the burden of justifying a rejection sits with the insurer. So a denial should never be a straight-through decision. It should be a recommendation with the reasoning surfaced to a human who owns the call, and the evidence attached.*
>
> *So I'd build the automation asymmetrically: automate approvals aggressively behind guardrails, and treat denials as decision-support. That's not a limitation of the technology — it's the correct design for a regulated decision."*

**If the role is at ICICI Lombard or any insurer, add the regulatory fact:**

> *"And the regulator has effectively already written that policy. The IRDAI Master Circular on Health Insurance Business requires that no claim be repudiated without approval of the Policyholder Protection Committee or a three-member Claims Review Committee. So auto-decline isn't just unwise — it isn't available."*

*(Source: IRDAI/HLT/CIR/PRO/84/5/2024, dated 29.05.2024 — verified in `health_claims_domain_research.md`. Do not cite a circular number you have not checked.)*

### Claim 4 — The explanation comes from the trace

**Your best technical position. Understand why it is right.**

> *"The decision trace has to be the source of the explanation. If you ask a model to explain a decision it didn't structurally make, you get a plausible narrative that isn't the actual reason. The model will produce a fluent, confident, well-structured justification — and it will be a reconstruction, not a record.*
>
> *So the system records the rules that fired, the inputs used, the model versions and the outcome, and the explanation is generated from that record. In a regulated decision, a plausible explanation that isn't the real one is worse than no explanation at all — because it survives review."*

**The follow-up you will get: "How is that different from logging?"**

> *"A log is written by the process about itself, and the process can be wrong or the log can be edited. A trace is the decision's own structure — which rules fired and on what inputs. The difference is that the trace can be replayed and the decision reproduced. A log tells you what the process said it did."*

### Where this principle can go wrong

**Do not let it sound like you are anti-automation.** The position is *automate aggressively where it is safe*, not *be cautious everywhere*. If you sound risk-averse, you read as someone who will not ship.

> *"I'm not arguing for less automation. I'm arguing for asymmetry — push hard on approvals, be deliberate on denials. The automation rate is the metric most likely to be optimised for its own sake, and a high automation rate on denials is a regulatory problem wearing a KPI."*

---

## §2 — Principle 2: "Deterministic where it is contractual, model-based only where judgement is required"

> *"Cost gates sit before the model, not around it."*

### What it means

Two claims:

1. **Some decisions are computable, and those should never touch a model.** Policy coverage is a contract. A contract is arithmetic and rules. A probabilistic answer to a contractual question is indefensible in an audit.
2. **The cheap filter goes before the expensive one** — not as an optimisation bolted on later, but as the architecture.

### How to explain it

> *"In JobAgents, scoring is pure arithmetic and string matching — five weighted components, no model call anywhere. Twenty-two thousand eight hundred and thirty-nine scores computed with zero model calls, and only the top hundred and fifty-five above threshold ever reach an LLM.*
>
> *That's the pattern I default to. If I'd asked a model to judge every posting, cost would scale with sourcing volume — and sourcing volume is the one thing the pipeline exists to maximise. Retrofitting a gate onto a system that already calls a model per item is much harder than building the gate first."*

### Why the ordering matters — the insight

> *"The obvious design is to put a model in the loop and add a filter afterwards if cost becomes a problem. That's backwards. The gate has to be the first thing, because by the time you've built the model path you've built a system whose economics depend on the model being there."*

### The follow-up: "Isn't a rules engine brittle?"

> *"A rules engine is exactly as brittle as the rules — which is a feature, because you can read them, test them and fix them. A model is brittle in ways you can't enumerate. For anything contractual I'd rather have a rule I can point at in an audit than a probability I can't explain."*

### Where it can go wrong

**Do not say "never use a model for decisions."** That is not your position and it is not credible.

> *"Models are the right tool where judgement is genuinely required — document interpretation, summarisation, surfacing inconsistencies. They're the wrong tool where the answer is defined by a contract or a rule."*

---

## §3 — Principle 3: "Bounded autonomy with an explicit human boundary"

> *"Retries are capped, escalations are defined, budgets and kill switches exist, and a no-result outcome is a valid recorded result."*

### The four elements, each with evidence

| Element | What it means | Your evidence |
|---|---|---|
| **Retries are capped** | Transient failure gets a second chance; unresolvable cases do not get infinite attempts | The data-quality agent: **3 retries**, then escalate |
| **Escalations are defined** | The terminal state for an unresolvable case is a specific human, not silence | Email escalation when the agent cannot resolve a domain |
| **Budgets and kill switches exist** | Hard limits the agent cannot exceed, and a way to stop it | `MAX_SPEND_USD`, `MAX_TURNS_PER_AGENT`, `MAX_WALL_CLOCK_MINUTES`, and a `STOP` file halting hunters at the next turn boundary |
| **A no-result outcome is valid and recorded** | Finding nothing is a legitimate result, not a failure to be hidden | BugAgents: a no-finding verdict is recorded |

### How to explain it

> *"Autonomy without a boundary isn't autonomy, it's an unobserved process. So every system I build has three things: a cap on how long it can try, a defined human to escalate to, and a hard limit it cannot cross on spend or turns.*
>
> *The part people miss is the fourth: a no-result outcome has to be valid. If the only acceptable outcome is finding something, you've built a system with an incentive to fabricate. Making 'found nothing' a recorded, acceptable result is what lets the gate refuse thirty-four candidates and promote two without that looking like failure."*

### The line worth memorising

> *"The escalation path has to be cheap enough that using it isn't a punishment."*

**Why:** if escalating is expensive, slow or politically costly, people stop escalating and start guessing. The design has to make the safe path the easy path.

### The follow-up: "How do you decide where the boundary goes?"

> *"Two questions. Can this be undone cheaply? And is the case clearly covered by the rules? Reversible and covered — the system decides. Irreversible or not covered — a human decides. And I separate the item from the rule: I'll decide the item, because that's the job, but a gap in the guideline isn't mine to fill unilaterally, because my fix would only apply to me and would make my behaviour inconsistent with everyone else's."*

---

## §4 — Principle 4: "Disclosure over polish"

> *"Where a result is weak I publish the weakness — a B+ audit verdict, 34 refused candidates, a self-audit that found its own headline result circular. A system whose limits are documented is more useful than one that looks clean."*

### Why this is the differentiator

**Almost no candidate volunteers a weakness.** The instinct is to present the strongest version and hope the gaps are not found. This principle inverts that — and on a senior application, in a role that involves governance, it is precisely the trait being hired for.

### The three examples, and how to present each

**1. The B+ audit verdict.**
> *"I commissioned an independent numerical audit of AgentSwarm's output. It verified twenty-two of twenty-five quantitative claims exact, located all five defects, and returned the verdict B-plus — not publication-grade without that audit. That verdict is published alongside the work. I'd rather ship something whose weaknesses are documented than something that looks clean."*

**2. The 34 refusals.**
> *"Thirty-four candidates refused to promote two. On a dashboard that looks like a system that mostly fails. It's the number I'd defend hardest, because a filter that promotes everything has a refusal count of zero and no verification at all."*

**3. The circularity finding.**
> *"One of the agent-authored manuscripts had a self-audit attached that found its headline agreement was circular — the model's outputs were the input constants — and its second result was tuned. It recommended against submitting the paper. I didn't hide that; it's the single best evidence I have that the audit layer does real work rather than producing favourable verdicts."*

### The follow-up: "Isn't that just being negative about your own work?"

> *"No — it's the difference between a result and a claim. If I tell you a system works and I haven't tested where it breaks, you're relying on my optimism. If I tell you it works within these limits and here's the audit that found the edges, you can make a decision. The first is marketing. The second is engineering."*

### The follow-up: "Give me an example where you were wrong."

**This principle sets this question up, so have an answer ready.**

> *"Two. In JobAgents I built a scoring weight that interacted with a formula and made an entire role track return zero candidates. Nothing errored — the run completed and the summary looked fine. Absences don't throw. I only found it because a track reporting zero is suspicious.*
>
> *And in the data-quality agent I built the mechanism before the instrumentation, so I can't tell you the resolution hit rate. Both are the same lesson: I measured what was easy to measure rather than what mattered."*

---

## §5 — How the four principles fit together

They are not four separate opinions — they are one argument:

> *"The four are connected. **Deterministic where contractual** means the decision is computable. **Verification before autonomy** means you can prove what was decided and why. **Bounded autonomy** means the system knows its own limits and hands over at them. **Disclosure over polish** means you find out where the limits are before your users do.*
>
> *Put together: a system that can be trusted with a decision, because you can explain it, bound it, and show where it fails."*

**Say that paragraph if you get an open question like "what's your philosophy on AI systems?"** It is a complete, structured answer in five sentences.

---

## §6 — Practice set for this guide

| # | Question |
|---|---|
| 1 | What does "verification before autonomy" mean? |
| 2 | Should an AI system ever auto-decline a claim? |
| 3 | How is a decision trace different from a log? |
| 4 | Why put the cost gate before the model rather than around it? |
| 5 | Isn't a rules engine brittle compared to a model? |
| 6 | How do you decide where the human boundary goes? |
| 7 | Why do you publish your own B+ audit verdict? |
| 8 | Tell me about a time you were wrong. |
| 9 | What's your philosophy on building AI systems? |
| 10 | You sound cautious about automation. Will you ship? |

**Question 10 is the trap.** If any answer makes you sound risk-averse rather than deliberate, correct it: *"I'm arguing for asymmetry, not caution. Push hard where it's safe, be deliberate where it isn't."*

---

*← Guide 4: Selected Systems · Guide 6: Question Bank →*
