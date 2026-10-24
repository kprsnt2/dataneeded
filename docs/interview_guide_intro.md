# Interview Guide — Projects, Wording, and the Reasoning Behind Them

This guide exists because a resume bullet is a *claim*, and an interview is where
you have to defend it. Every project below is broken into the same four
questions, so you can rehearse the shape rather than memorise prose:

| Question | What it prepares you for |
|---|---|
| **Why I built it this way** | "Walk me through this." The design rationale, and the problem that forced it. |
| **Limitations** | "What doesn't it do?" The honest boundary. Volunteering this builds credibility fast. |
| **What I'd improve with no restrictions** | "What would you do with more time/compute?" Shows you know the gap and have a plan. |
| **Alternatives not chosen, and why** | "Why not use X?" Shows the decision was deliberate, not the only option you knew. |

---

## The one rule

**Every number in this guide traces to `config/profile.md`.** That file is the
single source of truth, and it was reconciled against the live deployed sites on
2026-10-11. If a figure is not in that file, do not say it out loud.

The specific trap: the engineering blog posts under `docs/blog/` were written
earlier and contain **superseded** figures. They are good for *narrative* — why
something was built, what broke — but their numbers are stale. Read them for the
story, take the numbers from `config/profile.md`.

`config/profile.md` also carries a binding **"Stale values — do not use"** list.
Treat anything on it as deleted. If an interviewer quotes an old number back at
you (from a cached page or an old copy of your resume), the correct move is:
*"That figure is superseded — the current number is X, from the live dashboard."*

---

## How to use this

1. **Read it once, fully**, a day or two before. Do not try to memorise it.
2. **Before the interview**, read only the four headings per project and the
   *resume wording* block. That is your trigger list.
3. **Say numbers slowly.** "Fifteen thousand three hundred and seventeen tool
   calls" lands. A mumbled figure invites doubt.
4. **Volunteer one limitation per project.** It is the single strongest signal
   that you understand your own system, and it pre-empts the question.
5. **Never say "we"** about solo work. These are yours — say "I built".

---

## The projects, in the order they appear

| Project | One-line framing |
|---|---|
| **JobAgents** | A job pipeline that refuses to fabricate — deterministic matching as a cost gate, and code-enforced anti-fabrication guards. |
| **BugAgents** | Two autonomous security-research agents behind an evidence gate: 34 findings refused, 2 promoted. |
| **AgentSwarm** | A research arena whose audit ledger lives outside the agents' writable directory — plus the two papers it produced. |
| **AI Eco** | Ten agents under hard, enforceable limits: bounded memory, zero-false-positive pruning. |
| **BrandXY** | Fine-tuning a 20B model to measure and steer recommendation bias. |
| **Project Awakening** | Long-horizon autonomous behaviour and recovery across a 330-turn API blackout. |
| **mSeat** | A combinatorial allocation simulator validated against published official results. |

---

## Two things to be careful about

**BugAgents disclosure.** Name the project and cite aggregate counts and
severities only. Do **not** name the vendor, program, asset, repository, or
vulnerability class — those reports are submission-ready drafts and nothing has
been submitted. If pushed for detail, the good answer is: *"I'm keeping specifics
private until the disclosure process completes, but I'm happy to walk through the
verification gate that validated them."* That answer is itself a demonstration of
security judgement.

**The papers are not your authorship.** The AgentSwarm manuscripts are authored
by the swarm agents (`A001_DarkMatter` / `A002_QuantumCosmos`). You built the
system that produced them. Paper 1 is published as a **Zenodo preprint** — not
peer-reviewed, not a journal publication. Paper 2 is a **manuscript that was not
submitted**, and its own self-audit found its headline results circular and
tuned. Claiming more than that is the fastest way to lose an interview with
anyone technical.

---
