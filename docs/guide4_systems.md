# Senior Resume — Interview Guide 4 of 6: Selected Systems

**Covers:** MyLocalCLI, rAsh Score, BugAgents, AgentSwarm, JobAgents, and the "Also shipped" line — every claim.

> **Framing rule for all five.** These are **independent, self-directed projects** — not employer work. Say it explicitly and early: *"these are my own projects, not client work."* Let them find out later and it reads as inflation. Say it first and it reads as precision.

---

## §1 — MyLocalCLI — Local-First Agentic Coding Assistant

> *Node.js, CLI, 8 providers* · Published on npm **v4.0.2** · **42 built-in tools**, **38 dynamic skills**, **8 providers**, **5 specialised sub-agents** · Parallel tool dispatch via `Promise.all`; provider failover.

### The 30-second pitch

> *"An open-source terminal coding agent published on npm — a Claude Code alternative built around local and free-tier models. Forty-two built-in tools, thirty-eight dynamic skills, eight providers, five specialised sub-agents. The engineering decisions I'd point at are parallel tool dispatch and provider failover."*

### What it is, step by step

1. **What it is** — a CLI coding assistant. You install it with `npm install -g mylocalcli` and run it as `mlc` or `mylocalcli`.
2. **Why local-first** — it runs against local models (Ollama, LM Studio, vLLM) or free tiers (OpenRouter, Groq), so there is no mandatory paid subscription and no telemetry.
3. **What makes it agentic** — 42 tools the model can invoke, 38 skills auto-injected into the system prompt when matching project files are detected, and 5 sub-agents for specific jobs (code reviewer, explorer, test generator, refactorer, doc writer).
4. **The distribution point** — it is **published on npm**, which means anyone can install it. That is a different bar from a repo.

### The three engineering points to lead with

**1. Parallel tool dispatch.**
> *"Older assistants block sequentially on every tool call — read a file, wait, read another, wait. MyLocalCLI dispatches concurrent calls using `Promise.all`, so the model can read multiple files, search text and run diagnostics simultaneously. On a real task that is the difference between a few seconds and a long wait."*

**2. Provider failover.**
> *"Eight providers wired, with automatic fallback when one hits rate limits, context overflow or a dropped connection. And a deliberate rule: models are never silently swapped. If you asked for a specific model, you get that model or a clear failure — not a quiet substitution that changes your results."*

**3. Skills as context injection.**
> *"Thirty-eight skills that auto-inject best-practice instructions when matching project files are detected. A Python file pulls the Python skill into the system prompt. It's contextual grounding rather than one giant prompt."*

### Likely follow-ups

| Question | Answer spine |
|---|---|
| *"Why build this when Claude Code exists?"* | Cost and privacy. It runs on local models with no telemetry and no subscription. And building it taught me the harness internals — tool dispatch, context management, provider abstraction. |
| *"How do you handle context limits?"* | Tool results are the bulk of context. Read line slices rather than whole files, search before reading, and summarise aggressively. |
| *"Is it used by anyone?"* | **Do not invent users or download counts.** *"It's published publicly on npm and the portal is live. I'm not claiming adoption figures."* |
| *"What's the hardest part?"* | Provider abstraction — eight APIs with different shapes for the same operation. That is where most of the bugs live. |

### Where it can go wrong

**Naming "6 providers"** — the README documents **8**. Use 8. And note that vLLM is documented but not in the provider config, so if asked precisely: *"eight are documented; seven are in the provider registry, with vLLM as a documented self-hosted path."*

### The honest limit

> *"It's a single-maintainer project. No test coverage to the standard I'd want in a team codebase, and the provider abstraction is where the fragility sits. It works, it's published, and it's not production-hardened for an enterprise."*

---

## §2 — rAsh Score — Multi-Model AI Brand-Visibility Index

> *Next.js, Turso/LibSQL, GitHub Actions, Vercel* · **4 providers** · **300 tracked brands across 20 industry cohorts** · **4 independent dimensions** · daily pipelines · multi-agent debate arena · text-to-SQL chat.

### The 30-second pitch

> *"A live multi-model evaluation platform. It queries four providers — ChatGPT, Gemini, Claude, Groq — with standardised prompts, and scores three hundred brands across twenty industry cohorts on four independent dimensions: recommendation, sentiment, prominence and factual accuracy. Daily pipelines run on GitHub Actions, writing into Turso, surfaced through a Next.js dashboard on Vercel."*

### Why this matters more than it looks

**This is a multi-model evaluation harness with a published rubric.** That is the same class of system as judging whether any AI system is behaving correctly — which is exactly the skill senior AI roles are hiring for.

> *"The reason I'd point at this one: it forced me to solve the problem of getting comparable, structured output out of models that all answer differently, and detecting when a model update changes the answer. That's an evaluation problem before it's a product."*

### The four dimensions, explained

| Dimension | What it measures |
|---|---|
| **Recommendation** | How frequently and authoritatively models suggest the brand |
| **Sentiment** | The reputation tone in the answers — positive, neutral, negative |
| **Prominence** | How early and visibly the brand appears in generated rankings |
| **Accuracy** | The factual precision of the model's knowledge about the brand |

**Scored independently, each 0–100, composed into a visibility score.** The point of independence: a brand can rank highly but be described inaccurately, and collapsing those into one number would hide it.

### Likely follow-ups

| Question | Answer spine |
|---|---|
| *"How do you compare models fairly?"* | Standardised prompts — identical inputs across providers, so the variance you observe is the model's, not the prompt's. |
| *"How do you detect model drift?"* | The daily cadence is the detector. A fixed prompt set run on a schedule means a model update shows up as a score movement you can see, rather than something you discover when a user complains. |
| *"What did you learn about the models?"* | **Only say what you have actually observed in your own data.** You have 300 brands across four models — you have real observations. Do not generalise into claims about model quality you cannot support. |
| *"Is 300 brands a lot?"* | It is 20 industry cohorts, which is the useful denominator. **Live site is the authority: 300 brands, 20 cohorts.** |

### Where it can go wrong

**Cite the live figures: 300 brands / 20 cohorts.** Your README says 279 / 19 and there is a **legacy domain (`bs.kprsnt.in`) still serving an older build at 285 / 19**. If anyone looks at the wrong link they see different numbers. Know this so you are not caught out:

> *"The live index at rashscore.live is the current build — 300 brands across 20 cohorts. There's an older domain still resolving with a previous dataset; I should retire it."*

**That answer turns a potential inconsistency into evidence you know your own deployment.**

---

## §3 — BugAgents — Evidence-Gated Autonomous Security Research

> *Python/Node, multi-harness orchestration* · **report promotion gate** (4 conditions) · **2 promoted / 34 refused** · per-turn tool-call auditing · **22 hunt runs / 84 agent turns / 15,317 tool calls** · **8 findings across 14 CWE classes**.

### This is your strongest project. Lead with it.

**The premise to state first:**

> *"There's no shortage of agents that can write a vulnerability report. Give a capable model a codebase and it produces something that looks like a finding — title, severity, CWE, impact paragraph, suggested fix, correctly formatted. And a meaningful fraction of the time it's wrong. The artifact looks identical either way. Only the evidence distinguishes them. So my question was narrower than 'can agents do security research' — it was: can I build a system where a report cannot be produced unless a bug was actually found?"*

### The promotion gate — the core answer

**Four conditions, all must hold:**

| Condition | What it kills |
|---|---|
| **Scope match** | Real bugs in software the program does not cover — technically correct, commercially worthless |
| **HEAD (commit) match** | A report that was true when written and false by the time anyone reads it |
| **Non-empty reproduction** | The agent emitting a `## Reproduction` heading followed by a description of what a repro *would* look like |
| **Evidence files exist** | A report citing `path/to/file.py:412` where the file does not exist, or is shorter than 412 lines |

**The line that makes it land:**

> *"The gate is the only component that checks a claim against the world instead of against other claims. Without it you have a system that produces well-formatted assertions and calls them findings. With it you have a system that mostly produces nothing — and occasionally produces something true. I care much more about the second property."*

### The refusal count — your best number

> *"Thirty-four candidates were refused to promote two. More than four times as many refused as promoted. It would be easy to read that as a system that mostly fails. I read it as the only number that tells me the gate is real. **A filter's job is to refuse. A system that never refuses candidates isn't filtering — it's transcribing.**"*

### Per-turn tool-call auditing

> *"After every turn the harness replays the agent's captured tool calls. Any host outside program scope plus the tooling allowlist aborts the agent. Any offensive tool — nmap, sqlmap, ffuf, nuclei — aborts the agent. Not warned, not logged-and-continued. Aborted. And it isn't theoretical: a live run was aborted exactly this way when a hunter reached for a build host that wasn't on the allowlist. **A safety control that has only ever been exercised by its own unit test is an untested control.**"*

### Likely follow-ups

| Question | Answer spine |
|---|---|
| *"Were the findings real?"* | *"Each has a reproducing proof of concept, a pinned commit and `file:line` citations. Whether they're novel I can't claim — the gate checks corroboration, not novelty."* |
| *"Did you report them?"* | **Nothing has been submitted.** *"They're submission-ready drafts. Submission needs my identity and acceptance of the program's terms, so it stays a manual action."* |
| *"Which vendor? What class?"* | **Refuse.** *"I'm keeping specifics private until the disclosure process completes, but I'm happy to walk through the verification gate that validated them."* **That answer is itself a demonstration of security judgement.** |
| *"How do you know the gate isn't just rejecting good work?"* | *"I don't, and that's the honest limit. The gate raises the floor — it checks four things. A report can pass all four and still be a bad report. It doesn't guarantee the ceiling."* |

### The hard limits — volunteer these

1. **Nothing has been submitted.** No finding has been triaged, accepted, or rewarded.
2. **No claim of novelty.** The gate checks corroboration, not prior art.
3. **No claim of coverage.** 22 runs against a bounded target set is a bounded search.
4. **The severity distribution describes what the gate accepted**, not anyone's security posture.
5. **One seat is filtered by the model provider** non-deterministically — the identical prompt returned blocked, pass, pass, blocked across four consecutive attempts.

---

## §4 — AgentSwarm — Auditable Multi-Agent Research Arena

> *Node.js, 4 harnesses, hash-chained ledger* · **34 runs, 35/35 hash chains intact** · ledger **outside** the agents' writable directory · **0 violations across 1,254 tool calls** · **0 of 2 self-assessing agents overclaimed** · **22 of 25** claims verified exact · verdict **B+**.

### The 30-second pitch

> *"An autonomous research arena where the interesting engineering was not getting the agents to produce output — it was the layer that decides whether to believe them. Every turn is written to a hash-chained ledger that sits outside the agents' own writable directory, so the thing being audited cannot alter the record of what it did. An independent oracle re-checked every turn for fabricated numbers and phantom artifacts: zero violations across twelve hundred and fifty-four tool calls."*

### The two ideas worth explaining

**1. The ledger is outside the writable directory.**

> *"A log the process writes about itself is not an audit — the process can edit it. The ledger lives outside the agents' writable area, and each entry hashes the previous one, so altering history breaks the chain. Thirty-four runs, all thirty-five chains intact."*

**2. Measured honesty, not asserted honesty.**

> *"I didn't ask the agents whether they had done good work — that's the untrusted input. An independent oracle checked every turn, and separately, two agents self-assessed their own scores: both claimed exactly the score they had independently earned. Zero overclaiming. That's a measured result about agent honesty rather than a claim about it."*

### The audit verdict — volunteer it

> *"I commissioned an independent numerical audit of the output. It verified twenty-two of twenty-five quantitative claims correct to the printed digits, located all five defects, and returned the verdict B-plus — not publication-grade without that audit. I publish that verdict alongside the work."*

**Why volunteering this is powerful:** almost no candidate reports their own audit grade. On a senior application it reads as exactly the trait being hired for — *disclosure over polish*.

### Likely follow-ups

| Question | Answer spine |
|---|---|
| *"What did the swarm actually research?"* | Nine domains; the visible output is cosmology manuscripts. **Do not lead with the physics.** If asked: the point is the pipeline and its audit, not the subject matter. |
| *"Are the papers yours?"* | **No.** *"The authors are the swarm agents `A001_DarkMatter` and `A002_QuantumCosmos`. I built the system that wrote them. Paper 1 is a Zenodo preprint — not peer-reviewed. Paper 2 was not submitted."* |
| *"Why B+?"* | The audit found five defects, all in markdown prose rather than Python modules. And Paper 2's self-audit found its DESI agreement circular and its S8 result tuned — it recommended against submission. |
| *"Isn't a self-audit that finds its own flaws just theatre?"* | *"It's the opposite — it's the pipeline catching its own overclaim. That's the single best evidence I have that the audit layer does real work rather than producing favourable verdicts."* |

---

## §5 — JobAgents — Deterministic Sourcing & Anti-Fabrication Pipeline

> *Python (stdlib only), SQLite* · **7,613 jobs / 5,854 distinct roles** from **10 sources** across **334 companies** · **1,759 duplicates** merged · **22,839 scores with 0 model calls** · guard catches **8/8 seeded fabrications**.

### The two points to lead with

**1. The cost gate sits before the model.**
> *"Scoring is pure arithmetic and string matching — five weighted components, no model call anywhere. It runs on every job for free, so only the top-N ever reach an LLM. Twenty-two thousand eight hundred and thirty-nine scores computed with zero model calls. If I'd asked a model to judge every posting, cost would scale with sourcing volume — and sourcing volume is the one thing the pipeline exists to maximise."*

**2. Anti-fabrication is enforced in code, not in a prompt.**
> *"The guard validates generated text against a ground-truth profile file before anything is written to disk. It catches eight of eight seeded fabrications. And what it actually caught in testing is the argument for it: a model attributed four of my independent projects to my employer as employment history. The prompt forbade exactly that, in capitals. The model did it anyway."*

### The line to deliver

> *"A prompt rule is a request — evaluated by the same model generating the content, in the same pass, under the same pressure to be fluent. A guard runs after generation, in code, has no opinion about plausibility, and fails loudly. **If the rule isn't enforced by something that can reject the output, it isn't a rule — it's a suggestion.**"*

### Likely follow-ups

| Question | Answer spine |
|---|---|
| *"Why stdlib only?"* | Zero dependencies is a feature when the whole thing runs unattended on a schedule. Nothing to break, nothing to upgrade. |
| *"How does two-layer dedupe work?"* | Layer one is a `UNIQUE(source, external_id)` constraint — same posting, same source. Layer two is a `company|title` key that **links** rows without deleting them, so provenance survives. |
| *"What's the biggest gap?"* | *"The funnel ends at 'approved'. There's no Sent stage and no Replied stage, because the system has no idea either happened. I measured the top of the funnel to the unit and the bottom not at all."* |
| *"What's the failure mode of the guard?"* | *"It catches structural violations — an invented employer, an uncited figure, a withheld term. A confidently-stated false metric shaped like a real one still passes. That gap is real and it is not closed."* |

---

## §6 — "Also shipped"

> *AI Eco (10-agent swarm, FastMCP server, <4,000-word bounded memory), BrandXY (GPT-OSS-20B LoRA fine-tune, 76.5% vs 25.5% baseline), Project Awakening (1,441 autonomous turns, 100% CI integrity through a 330-turn API blackout), mSeat (18,000+ candidate allocation simulator, validated within 73 ranks of official cutoffs).*

**One line each, only if asked:**

| Project | The one thing to say |
|---|---|
| **AI Eco** | *"Ten agents running scheduled CI/CD with living memory bounded under four thousand words. The bound is the point — unbounded state makes behaviour a function of history rather than purpose."* **Limit:** 83.4% is a self-defined fitness function, not an external benchmark. |
| **BrandXY** | *"Fine-tuned GPT-OSS-20B on AMD MI300X to quantify and steer recommendation bias — 76.5% against a 25.5% baseline, under multi-model A/B evaluation. Open weights released."* **Limit:** single run, no external replication. |
| **Project Awakening** | *"1,441 autonomous turns and 1,553 commits, holding 100% CI integrity through a 330-turn cloud API blackout with no human intervention."* **Limit:** one run. |
| **mSeat** | *"A combinatorial seat-allocation simulator across 59 colleges and a seven-dimensional reservation matrix, validated within 73 ranks of the official cutoff at 90.6% dataset compression."* **Limit:** one phase; a validation exercise, not a deployed product. |

**Do not open with these.** They are depth if the conversation goes there.

---

## §7 — Practice set for this guide

| # | Question |
|---|---|
| 1 | Walk me through BugAgents. What does the gate do? |
| 2 | Why is 34 refusals a good number? |
| 3 | Which vendor did you find bugs in? *(Refuse gracefully.)* |
| 4 | Explain AgentSwarm's ledger. Why outside the directory? |
| 5 | Your own audit graded it B+. Why publish that? |
| 6 | What is rAsh Score measuring, and how do you compare models fairly? |
| 7 | What's MyLocalCLI, and why build it? |
| 8 | In JobAgents, why zero model calls in scoring? |
| 9 | How does the anti-fabrication guard work, and what does it miss? |
| 10 | Which of these is your strongest work, and why? |

---

*← Guide 3: Professional Experience · Guide 5: Approach →*
