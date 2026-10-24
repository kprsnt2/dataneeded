# Agent Systems — An Engineering Record

This series is the build record of three autonomous-agent systems I designed and
built independently — a job-sourcing pipeline, a multi-agent research arena, and
a pair of security-research agents — written up against what the code and the
live deployments actually show rather than what the pitch decks of the genre
promise. Each post covers one system end to end: the design decision that turned
out to matter, the bugs that cost real time, the guardrails that are enforced in
code rather than requested in a prompt, and the limitations that remain. The
systems are independent projects; none of this is employer work.

---

## The posts

| # | Post | What it covers |
|---|---|---|
| 01 | [JobAgents: a job pipeline that refuses to fabricate](01-jobagents.md) | ATS-first sourcing, deterministic matching as a cost gate, two-layer dedupe, and an anti-fabrication guard that caught a real model output. |
| 02 | [AgentSwarm: 34 runs under an oracle that cannot be edited](02-agentswarm.md) | A multi-agent research arena whose forensic ledger lives outside the agents' writable directory, so the audited cannot edit the audit. |
| 03 | [BugAgents: two agents hunting real bugs, and the gate that stops them overclaiming](03-bugagents.md) | Two autonomous research agents, a promotion gate that blocks unverified findings, and why disclosure safety is a code rule. |
| 04 | [The bugs that cost real time](04-engineering-findings.md) | Silent failures across four agent CLIs — the defects that reported success while producing nothing usable. |
| 05 | [What the swarm actually found (and what it got wrong)](05-what-agents-discovered.md) | The output of the runs, read honestly: what held up, what did not, and where the harness misled. |

---

## How to read this

Every number in this series is traceable to one of two places: a live site, or an
artifact in the repository that produced it. Nothing is rounded up, estimated, or
extrapolated, and where a figure is a snapshot it is labelled with the time it was
taken. Where a claim could not be verified, it is either stated as unverified or
left out.

That constraint is deliberate. Agent systems produce a lot of confident-sounding
output, and the easiest way to write about them is to repeat the output. The
harder and more useful thing is to separate what was measured from what was
merely generated — which is the same discipline the systems themselves needed in
order to be worth running.

Expect file-and-line references, real command output, and limitations sections
that are not hedged. Where a design decision was wrong and later corrected, the
correction is in the post next to the original claim.

---

## Live deployments

| Site | System |
|---|---|
| [job.kprsnt.in](https://job.kprsnt.in) | JobAgents — sourcing, matching, and pipeline numbers |
| [agent.kprsnt.in](https://agent.kprsnt.in) | AgentSwarm — the research arena and its runs |
| [bug.kprsnt.in](https://bug.kprsnt.in) | BugAgents — the work, not the findings |

The BugAgents site is deliberately scoped to show the *process* and aggregate
counts. Its findings are not public: no target names, no vulnerability detail, no
reproduction steps, pending coordinated disclosure.

---

*Source repositories and configuration are referenced inline in each post. The
numbers in post 01 come from the JobAgents pipeline database and the snapshot
published at `job.kprsnt.in`.*
