# Periskope application — answers

> Every figure here traces to `config/profile.md` (reconciled against the live
> deployed sites). Nothing is invented. Independent projects are labelled as
> independent — they are not employer work.

---

## Q1. Top AI projects (Option 2 — written)

I'll give you two, one paid production work and one independent system, because
they show different things.

### Project 1 — AgentSwarm: an autonomous multi-agent research arena (independent, self-directed)

**What it is.** Four CLI agent harnesses (agy, omp, pi, step) driving Gemini-class
models, set loose unattended on real research questions — with an adversarial
oracle checking every turn, and a SHA-256 hash-chained ledger recording every tool
call, parameter, reasoning token and file diff. Live: https://agent.kprsnt.in

**My exact contribution.** Sole architect and builder. I wrote the turn loop, the
oracle, the ledger, and the harness that makes four different agent CLIs behave
identically enough to be comparable.

**Models and AI stack.** Node.js orchestration across four local agent CLIs;
Gemini 3.8 Flash class models; an adversarial dual oracle (transcript-level and
artifact-level); SHA-256 hash-chained forensic ledger; independent verifier
processes for scoring.

**Key technical decisions.**
1. **The ledger lives outside the agents' writable directory.** The audited cannot
   edit the audit. Deleting a file shows up as a positive signal, not an absence.
2. **An independent oracle, not self-assessment.** Agents cannot grade their own
   work — I moved verification outside the actor, which is the whole design.
3. **Epistemic classification.** Each question is tagged empirical / engineering /
   exploratory / metaphysical. Asserting a verdict on an undecidable question is a
   *protocol violation*, not a wrong answer. An agent that says "we have
   conclusively proven X" on a metaphysical question trips the oracle.
4. **Hash chaining.** Retroactive edits to history are detectable by recomputation.

**Outcome.** 34 runs, **35/35 ledger hash chains cryptographically intact**, **0
oracle violations across 1,254 tool calls**, and **0 of 2 self-assessing agents
overclaimed** — each claimed exactly the score it had independently earned. An
independent numerical audit verified **22 of 25 quantitative claims** correct to
the printed digits, with every defect in prose rather than code. Agent-written
test suites pass **195/224** when I re-ran them myself in a fresh interpreter.

The swarm also produced **two agent-authored cosmology manuscripts** in REVTeX,
credited to the agents (`A001_DarkMatter` / `A002_QuantumCosmos` — I built the
system, not the physics). **Paper 1 is published as a Zenodo preprint**
(DOI [10.5281/zenodo.23232189](https://zenodo.org/records/23232189), 8 Oct 2026).
**Paper 2 was not submitted** — its own attached self-audit found its headline
DESI agreement *circular* (the model outputs were the DESI input constants) and
its S8 result *tuned*, and recommended against submission. I kept that audit in
the repository, because a pipeline that catches its own overclaim is the useful
result.

**Honest limitation.** The audit verdict on the research output is **B+ / not
publication-grade without that numerical audit**, and it is not peer-reviewed.
Only 2 of 4 agents self-assessed, and in that setup honesty was the cheapest path
to a full score — so "no overclaiming" is the *expected* outcome, not a
surprising one. A temptation task, where deception is cheaper than success, has
not been run.

GitHub: https://github.com/kprsnt2/AgentSwarm

---

### Project 2 — JobAgents: an AI pipeline that refuses to fabricate (independent, self-directed)

**What it is.** A multi-agent pipeline that sources roles from 10 public sources,
scores them deterministically, generates tailored resumes, and drafts outreach —
with code-enforced guards that block fabricated content before it reaches disk.
Live: https://job.kprsnt.in

**My exact contribution.** Sole builder. It runs on a schedule, and I own every
stage.

**Models and AI stack.** Python standard library only — **zero external
dependencies**, deliberately. Agent CLIs (omp) for the generation stages, SQLite
for state, and a deterministic scoring engine that uses **no model at all**.

**Key technical decisions.**
1. **Deterministic scoring as a zero-cost gate.** I compute **22,839 match scores
   with 0 model calls**, and only candidates above the score-65 threshold reach an
   LLM. The expensive path is rationed by arithmetic, not by hope.
2. **Anti-fabrication enforced in code, not in the prompt.** Generated Markdown is
   parsed into structural invariants *before* anything is written. I originally
   tried to solve this with prompt instructions and the model ignored them — it
   credited my side projects to my employer. So I moved the rule into code.
3. **Two-layer dedupe.** **1,759 duplicate postings** collapsed, so the same role
   from three sources doesn't become three applications.
4. **No send path, by design.** The pipeline can draft, never transmit. A human
   approves every message.

**Outcome.** **7,613 jobs / 5,854 distinct roles** from 10 sources across 334
companies. The anti-fabrication guard catches **8/8 seeded fabrication classes**
and has caught real model hallucinations. Review invariants: 0 failures.

**Honest limitation.** Salary coverage is ~21% of postings, so compensation can't
drive ranking. Dedupe is lexical, so a reworded repost can survive as a distinct
row. And it is a personal automation, not a product — no external users.

---

## Q2. What makes you stand out

**I build the part that decides whether AI is trustworthy, not just the part that
impresses.**

Concretely, on systems I built: a 4-point promotion gate that **refused 34
unverified findings** and promoted only the **2** the workspace could corroborate;
an anti-fabrication guard that parses generated Markdown into invariants before
disk write and catches **8/8** seeded fabrications; and a hash-chained ledger
**35/35 intact** that lives outside the agents' writable directory, so the audited
cannot edit the audit. Those are not prompt instructions. They are code that
refuses.

**Where that instinct comes from is the unusual part.** Before AI I spent **9 years
at Optum auditing federal CMS enrollment transactions for regulatory compliance**
— I was paid to find what doesn't reconcile, and to document it so someone else
could verify it. That is why my first instinct with a model is "what would make
this claim falsifiable" rather than "does the demo look good."

**I also ship and operate, not just prototype.** At Black Piano I own **18
automated ETL pipelines** feeding BigQuery and Looker Studio dashboards across
**18 industry sectors** for US and UK clients, plus a Gemini-powered self-healing
data-quality agent that resolves missing data, retries 3×, and **escalates to a
human by email only when it genuinely cannot resolve** — and a custom MCP tool
that lets non-technical marketing and sales staff generate data-grounded blog
posts from a one-line prompt.

**And I measure my own work honestly.** I published the **B+ / not
publication-grade** verdict on my own research output, and I kept an audit that
found my own paper's headline result circular. I'd rather be the engineer who
tells you the system is weaker than it looks than the one who finds out in front
of your customers.

Two years of hands-on agent work, 9 years of compliance discipline, and a habit of
building the gate before the feature.

---

## Q3. What interests me about Periskope

**Your core bet is the one I've spent two years on: making a platform reliable
that was never designed to be automated.**

"No WhatsApp Business API required" is the most interesting line on your site. You
are connecting regular WhatsApp numbers, managing group chats and multi-number
inboxes, with no template approval and no per-message cost — which means you've
had to absorb a platform's undocumented behaviour and make it dependable anyway.
That is exactly the class of problem I work in. The agent CLIs I orchestrate have
failure modes that *report success while producing nothing*: one silently hangs
forever if its stdio is piped, one consumes the next token as its prompt, another
has no working-directory flag and just hangs. I built a harness that absorbs all
of it so the system stays reliable. Your 5-minute, no-Business-API onboarding is
that same discipline pointed at WhatsApp.

**"Train Periskope Agent on Your Data" is a problem I've already built.** At Black
Piano I built a Gemini-powered agent that resolves missing data via
reference-table lookup with LLM fallback, writes results back to both the dataset
and the lookup table, retries 3×, and **escalates to a human by email only when
unresolved**. The escalation boundary is the hard part — and it's precisely what
determines whether an AI agent answering your customers is an asset or a
liability.

**"Flag Important Messages with custom prompts" is a gate, and gates are what I
build.** Your customers will judge the AI by the tickets it raises *wrongly*. I
built a 4-point promotion gate that refused 34 unverified findings before
promoting 2, and an anti-fabrication guard that catches 8/8 seeded fabrications
before anything is written. Same shape: the model proposes, the code decides.

**The compliance side is where my background is genuinely unusual.** You're GDPR
compliant and ISO/IEC 27001 certified, and you sell "Data Exports and Logs" and
audit trails. I spent 9 years auditing federal CMS enrollment transactions under
regulatory rules, and I built a hash-chained audit ledger that lives outside the
agents' writable directory so the audited cannot edit the audit. Compliance-grade
logging isn't a feature I'd have to learn.

**And the scale is real work, not a demo.** 5,000+ businesses across 50+ countries,
1,000+ numbers — I've built the unglamorous half of that: 7,613 postings and 5,854
distinct roles deduped across 10 sources, deterministically, with the expensive
model path rationed by a zero-cost gate.

I'd like to work on the reliability layer of an AI product where being wrong has
a customer attached.

---

## Q4. Where did I find this opportunity?

**ANSWER NEEDED FROM YOU.** This one is factual and only you know it.

Likely options — pick one and delete the rest:
- LinkedIn
- Company careers page
- A job board (Wellfound / Naukri / Instahyre / YC Work at a Startup)
- Twitter / X
- Referral (if so, name + contact, otherwise write **NA**)

If it was a referral, the form asks for their name and contact number so the
company can thank them — include it or write NA.
