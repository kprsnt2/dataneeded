# X / Twitter Threads

Four threads for the series. Each post is under 280 characters.

> **Note on the character counts.** Counts are labelled in brackets as a hand tally.
> They were verified by manual count, not by script (the shell was unavailable when
> these were written). The longest post in the file measures ~250 characters, so every
> post has at least 30 characters of margin against the 280 limit. Treat the labels as
> approximate guides, not exact figures — the margin is the thing that matters.

**Posting guidance**

| Question | Recommendation |
|---|---|
| Order | Post thread 1 (launch) first, then one project thread per day. Do not post all four in one day. |
| Best time | Tue–Thu, 09:00–11:00 IST. Engineering audiences on X skew US-morning, so 18:00–20:00 IST also works. |
| Attach an image | Yes — screenshot the live dashboard as post 1's image for threads 2–4. A number in a picture reads faster than a number in text. |
| Links | Put the live URL in the **last** post, not the first. Links in post 1 suppress reach. |
| Hashtags | 1–2 maximum, and only on the final post. `#AIagents` or `#LLM`. No hashtag walls. |
| Alt text | Always. Especially on dashboard screenshots. |

---

## Thread 1 — Series launch

**1/** [188 chars]
I spent the last few months building three autonomous agent systems and then trying hard to prove they were lying to me.

Two of them found real things. One of them found real bugs.

Writing up everything — the wins, and mostly the failures.

**2/** [246 chars]
JobAgents: a job pipeline that refuses to fabricate
AgentSwarm: 34 runs under an audit ledger the agents cannot edit
BugAgents: two agents hunting real vulnerabilities behind a verification gate

All three are live. All three publish their own numbers.

**3/** [259 chars]
The pattern across all three: the interesting engineering is not making the model produce output.

It is building the thing that decides whether to believe the output.

Every project ended up being mostly verification code. The model was the easy part.

**4/** [222 chars]
Some numbers:

22,647 job scores computed with zero model calls
35 ledger hash chains intact
15,317 tool calls across two security agents

None of those matter as much as this one: every single bug that cost me real time failed silently.

**5/** [201 chars]
Writing the whole thing up as a 5-post series — architecture, the bugs, what the agents actually discovered, and what the results do *not* prove.

Live now:

job.kprsnt.in
agent.kprsnt.in
bug.kprsnt.in

---

## Thread 2 — JobAgents

**1/** [243 chars]
A model wrote a resume for me that claimed four of my personal side projects were work I did for my employer.

The prompt explicitly forbade this.

The model did it anyway.

That one output changed how I build everything. Prompt rules are not guards.

**2/** [231 chars]
The fix was not a better prompt.

It was ~40 lines of code that walks the generated Markdown, tracks which employer section it is inside, and rejects the output if a project name appears as a bullet under an employer.

The resume never gets written. No human has to notice.

**3/** [238 chars]
Then I tested the guard against itself.

8 seeded fabrications: a fake employer, an invented "847%" figure, a fake job title, a fabricated user count.

All 8 caught.

A checker that only ever says "pass" is worthless. You have to falsify it.

**4/** [247 chars]
The other half is cost.

The matcher scores every job deterministically — 22,647 scores, zero model calls.

Only 274 candidates ever reach an LLM.

Scoring 7,549 jobs is free. That is the entire reason a daily run is affordable.

**5/** [241 chars]
Two-layer dedupe: same posting re-fetched, and same role on Greenhouse + LinkedIn + RemoteOK.

1,748 duplicate postings collapsed into one outreach target each.

Location is deliberately excluded from the key. One role in five cities is one email.

**6/** [235 chars]
The part I am least happy about: the pipeline measures the top of the funnel precisely and the bottom not at all.

It cannot tell me whether any of it worked.

The `applications` table exists in the schema. Nothing has ever written to it.

**7/** [190 chars]
Still, it runs unattended at 09:00 daily, and it has never sent a message on my behalf.

There is no send path in the code. That is structural, not a setting.

job.kprsnt.in

---

## Thread 3 — AgentSwarm

**1/** [240 chars]
I gave a swarm of agents real tool access, nine research questions, and 34 runs.

Then I put the audit ledger OUTSIDE the directory they could write to.

The audited cannot edit the audit. That single decision is the whole design.

**2/** [238 chars]
Before trusting a detector that reports "0 violations", I pointed it at deliberate deception.

A fake submission claiming "we solved it", with an out-of-range confidence value and two trivial tests, scored 60/100.

Honest, complete work scored 100/100.

**3/** [231 chars]
The instrument discriminates. That is the only reason "0 violations" means anything.

An uncalibrated checker reporting zero is not evidence of honesty. It is evidence of an untested checker.

**4/** [244 chars]
Then I had every quantitative claim independently recomputed.

22 of 25 verified correct.

And here is the part I did not expect: every single error was in markdown prose. Zero errors in the Python modules.

The opposite of the usual LLM failure mode.

**5/** [236 chars]
The arithmetic underneath was sound. The agents broke things when transcribing results into narrative — a factor-of-2 slip, two different physical quantities sharing one name.

Fluent prose, correct code. Not the failure mode I was watching for.

**6/** [246 chars]
Best story from the run:

One agent was asked whether Hindu gods are real. The domain is classed metaphysical, so asserting a verdict is a protocol violation.

It refused to rule, and formalised why: Bayes factor = 1.0. Zero bits of information.

**7/** [238 chars]
Its conclusion: the claim is not false. It is evidence-insensitive.

No observation could shift a rational credence either way.

That is a structural property of the claim, not a gap in current science. The firewall held across three agent identities.

**8/** [242 chars]
Honest caveat, because it matters: the audit verdict is B+ / not publication-grade without that numerical audit.

Agent-reported test counts are self-asserted. Where I re-ran the suites myself, 195 of 224 passed.

Claims, not measurements.

**9/** [180 chars]
34 runs. 35 ledger chains intact. 520 artifacts. 202 finding blogs.

Most of the value was in the failures and the caveats.

agent.kprsnt.in

---

## Thread 4 — BugAgents

**1/** [240 chars]
There is no shortage of AI agents that can write a vulnerability report.

The hard part is an agent that only reports something it can actually prove.

I built two of them. Here is the gate that makes the difference.

**2/** [238 chars]
A report is promoted only when the workspace corroborates it:

- target is in scope
- commit HEAD matches
- a reproduction exists and is non-empty
- the evidence files actually exist on disk

Fail any one and the report does not promote.

**3/** [232 chars]
That is the line between a model that writes a report and an agent that found a bug.

Writing is cheap. Corroboration is not.

The gate is the deliverable. The agents are the easy part.

**4/** [245 chars]
Every turn also gets a tool-call audit. Any out-of-scope host or offensive tool aborts the agent immediately.

This is not theoretical — a live run was aborted exactly this way.

The guard fired on real behaviour, not in a test I wrote to make it pass.

**5/** [236 chars]
Results, aggregate only: 8 findings, 5 High/Critical, 14 vulnerability classes.

22 hunt runs. 84 agent turns. 15,317 tool calls.

2 reports promoted.

**6/** [233 chars]
And 34 filter refusals.

That number is the feature, not the failure. A system that refuses candidates is doing its job. An agent that promotes everything it writes is not verifying anything.

**7/** [247 chars]
Disclosure note: findings are under responsible disclosure. I am publishing counts, severity and vulnerability class only.

No targets, no reproduction steps, no vendor names. Those go to the affected vendors through their official channels, not to a blog.

**8/** [196 chars]
Still open: the findings are submission-ready, and none has been submitted yet.

That is a manual step, and it has a real deadline. Reported second is worth zero.

bug.kprsnt.in
