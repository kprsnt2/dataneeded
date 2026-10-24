# BugAgents: The Gate Between a Written Report and a Found Bug

*Part 3 of a five-part series on building autonomous agent systems and then trying hard to prove they were lying to me.*

> **Disclosure posture — read this first.**
> BugAgents findings are under responsible disclosure. This post publishes
> **aggregate research metrics only**: counts, severity, and vulnerability class.
> Technical detail, reproduction steps, evidence, and program communications are
> withheld while findings are under responsible disclosure, and are shared with
> affected vendors through their official channels.
>
> There is no vendor name, program name, asset or repository name, target URL,
> CVE identifier, reproduction step, or code excerpt from any finding anywhere in
> this post. The vulnerability class names appear only as aggregate categories,
> exactly as the live site already publishes them, and no class is tied to any
> specific vendor, asset, or target.

---

## The premise, and the thing that is actually hard

There is no shortage of AI agents that can write a vulnerability report.

Give a capable model a codebase and a prompt, and it will produce something that
looks like a finding: a title, a severity, a CWE, a paragraph about impact, a
suggested fix. It will be formatted correctly. It will read like the reports you
see in public disclosure archives. And a meaningful fraction of the time, it will
be wrong — a misread of a helper function, an assumed call path that does not
exist, a vulnerability class applied because it is plausible rather than because
it is present.

That failure mode is not a prompting problem. It is a structural one: text
generation and bug finding are different activities that happen to share an
output format. The artifact looks identical either way. Only the *evidence*
distinguishes them.

So the question I actually wanted to answer was narrower than "can agents do
security research?" It was:

**Can I build a system where a report cannot be produced unless a bug was
actually found?**

BugAgents is my attempt at that. It is an independent, self-directed project —
not employer work — and the live counters are published at `bug.kprsnt.in`.
Everything below is the system and the method.

## The pipeline

Two autonomous agents run against disjoint targets. The pipeline has five
stages, and each stage exists to kill a specific class of error:

| Stage | What it does | The failure it exists to prevent |
|---|---|---|
| 1 · recon | Clone, map the surface, identify candidate components | Hunting blind; wasting turns on unreachable code |
| 2 · hunt | Read code and form candidate findings | — (this is the only stage that is supposed to be creative) |
| 3 · verify | Attempt to falsify the candidate against the actual code | Confirming a plausible-sounding but absent bug |
| 4 · report | Draft the structured report with evidence | Unsupported claims entering the output |
| ✓ validate | **Promotion gate** — workspace must corroborate the report | A confident-sounding report that describes nothing real |

The interesting design decision is that stages 1 through 4 are *not* the
product. They are the cheap part. The gate at the end is the product.

## The report promotion gate

This is the core idea, and it is the difference between the two things the
premise conflates.

A report is only **promoted** when the workspace independently corroborates it.
Promotion requires all four of the following, checked against the filesystem and
the target's own state — not against the agent's summary of them:

1. **Scope match** — the target is inside the program's declared scope.
2. **HEAD match** — the commit the agent analysed is the commit the report cites.
3. **Non-empty reproduction** — a reproduction exists and has content.
4. **Evidence files exist** — every file the report references is actually on disk.

Fail any one of those and the report does not promote. It does not get a warning
label, or a confidence score, or a "needs review" tag. It does not promote.

Why those four, specifically:

**Scope match** prevents the entire class of work that is technically correct and
commercially worthless — a real bug in software the program does not cover.

**HEAD match** is the one people skip, and it is the one that matters most. An
agent that clones a repository, analyses it, and then reports against a moving
branch can produce a report that was true when it was written and is false by the
time anyone reads it. Pinning the commit and verifying it means every claim is
anchored to a specific, immutable tree. It also makes the report independently
checkable by someone else, which is the whole point.

**Non-empty reproduction** is a low bar deliberately set low. It does not check
that the reproduction is *good*. It checks that the agent cannot satisfy the gate
with a placeholder — the failure mode where a model emits a `## Reproduction`
heading followed by a sentence describing what a reproduction would look like.
That reads as completeness and contains nothing.

**Evidence files exist** is the cheapest check and catches the most embarrassing
error: a report citing `path/to/file.py:412` where the file does not exist, or
exists and is shorter than 412 lines. This is the single highest-yield check in
the system. It is trivially cheap and it is not something a language model can
fake, because the filesystem is not in the model's context — it is the ground
truth the model has to be right about.

The philosophical point: a report is a *claim about the world*. The gate is the
only component in the system that checks a claim against the world instead of
against other claims. Without it, you have a system that produces
well-formatted assertions and calls them findings. With it, you have a system
that mostly produces nothing — and occasionally produces something true.

I care much more about the second property than the first.

## The scope guard: auditing every turn

The promotion gate is a filter at the *end*. The second control is at the
*beginning of every turn*.

Each agent turn's tool calls are audited. If a call touches an out-of-scope host,
or invokes an offensive tool, the agent is aborted immediately. Not warned,
not logged-and-continued — aborted.

This matters for two reasons. The obvious one is safety: an autonomous agent with
network access and a hunting objective is a system whose failure modes are not
confined to a text file. The less obvious one is that the guard is also a
*correctness* control. An agent that wanders outside its declared scope is an
agent whose findings cannot be promoted anyway — so aborting early is cheaper
than letting it produce work the gate will reject.

And this is not a theoretical control. **A live run was aborted exactly this
way.** The guard fired on real agent behaviour, in an unscripted run, not in a
test I wrote to make it pass. That distinction matters more than the feature
itself: a safety control that has only ever been exercised by its own unit test
is an untested control.

## Results — aggregate only

These are the counters the live site publishes. They are counts, severity, and
class. Nothing here identifies affected software.

**Findings: 8** — 5 High/Critical, 3 Medium.

**Vulnerability classes (14 distinct):**

| CWE | Class | Findings |
|---|---|---|
| CWE-22 | Path Traversal | 3 |
| CWE-284 | Improper Access Control | 2 |
| CWE-79 | Cross-site Scripting (XSS) | 1 |
| CWE-287 | Improper Authentication | 1 |
| CWE-1321 | Prototype Pollution | 1 |
| CWE-787 | Out-of-bounds Write | 1 |
| CWE-122 | Heap-based Buffer Overflow | 1 |
| CWE-125 | Out-of-bounds Read | 1 |

**Work performed:**

| Metric | Value |
|---|---|
| Hunt runs | 22 |
| Agent turns | 84 |
| Tool calls | 15,317 |
| Reports promoted | 2 |
| Filter refusals handled | 34 |
| Turns — harness `agy` | 43 |
| Turns — harness `omp` | 41 |

Two notes on reading these numbers honestly.

First, the severity distribution describes **findings the gate accepted**, not
the target's total risk. A count of 8 is a count of 8 things this specific system
was able to corroborate within a bounded number of runs. It is not an assessment
of anything's overall security posture, and it is not evidence of coverage or
completeness. Absence of a class in this table means this system did not promote
a finding in that class — nothing more.

Second, the two promoted reports are two *submission-ready* reports. Severity was
rated on CVSS, and the two High findings rated 9.3 and 8.6 — cited here as
aggregate severity figures only, attached to no vendor, asset, or class.

## Why 34 refusals is the feature

Here is the number I would defend hardest, and it is the one that looks worst at
a glance.

**34 filter refusals.** Thirty-four candidate findings were rejected before
promotion. That is more than four times the number of findings that survived.

It would be easy to read that as a system that mostly fails. I read it as the
only number that tells me the gate is real. Consider the alternative: a pipeline
that promotes everything it writes has a refusal count of zero, a findings count
equal to its candidate count, and no verification at all. It would look
*more* productive on every dashboard. It would also be worthless.

A filter's job is to refuse. A system that never refuses candidates is not
filtering — it is transcribing. The refusals are the work.

The same logic applies to the ratio that looks most disappointing: **2 promoted
from 8 findings.** That is not the gate losing six findings. That is the gate
distinguishing, across eight candidates, the two that the workspace could
actually corroborate. The gap between 8 and 2 is precisely the gap between a
report that was written and a bug that was found — which is the entire thesis of
this project, showing up as an operational counter.

I would rather ship a system that reports two things it can prove than eight
things it cannot.

## The open item, stated honestly

The findings are **submission-ready**. They have **not been submitted**.

That is a real gap and it is the most time-sensitive thing in this project. The
pipeline stops at "a report the workspace corroborates." Submission is a manual,
out-of-band action that no part of this system performs, and — a design error I
would fix first if I rebuilt it — nothing in it reminds me either.

The reason this is urgent is that vulnerability reports decay:

- **Programs close.** A program accepting reports today can reduce scope or stop
  accepting entirely.
- **Duplicates land first.** A valid finding reported second is worth
  approximately nothing. Value decays fast and non-linearly.
- **Disclosure obligations run on their own clock.** The longer a corroborated
  finding sits unreported, the worse the position if someone else finds it
  independently.

There is an important distinction here that I want to be precise about, because
it is the difference between a security process and a marketing one:
**submit, do not publish.** Submission goes to the affected vendor through their
official channel. The public site shows the *work* — the method, the gate, the
aggregate counters — and never the *findings*.

## What this does not prove

The limits matter more than the results, so I will be explicit.

- **No claim of novelty.** I do not know whether any of these findings are new. I
  have not compared them against prior art, and the gate does not check novelty —
  it checks corroboration. A real bug can be a known bug.
- **No claim that anyone has acted on anything.** No finding here has been
  submitted, triaged, accepted, or rewarded. No vendor has confirmed, fixed, or
  paid anything. The reports are drafts that pass a verification gate.
- **No claim of coverage or completeness.** 22 hunt runs against two targets is a
  bounded search. The 14 classes are what this system promoted, not what exists.
- **No claim that the gate is sufficient.** It checks four things. A report can
  pass all four and still be a bad report — a real bug with poor impact analysis,
  or a real bug in code the program considers out of scope by policy rather than
  by declaration. The gate raises the floor. It does not guarantee the ceiling.
- **No claim about scale.** Two agents, two targets, 84 turns. This is a working
  prototype of a verification discipline, not a research programme.

## What I actually took from building it

The model was the easy part. Getting a capable model to produce a plausible
vulnerability report took a prompt. Everything after that — the four gate
conditions, the per-turn audit, the refusal counting — is code whose entire job
is to disbelieve the model.

That is the same pattern as the other two projects in this series, and I did not
plan it that way. In all three, the model is a generator and the system's value
lives in the component that decides whether to believe the generator. Writing is
cheap and getting cheaper. Corroboration is not.

BugAgents is the sharpest version of that lesson because the stakes are
concrete: a plausible-sounding security report that describes nothing real wastes
someone else's time, and a real finding that sits unsubmitted wastes its own
value. The gate fixes the first problem. I still have to fix the second one
myself, on a calendar, before the clock runs out.

---

*Live aggregate counters and the disclosure notice: `bug.kprsnt.in`.*
*BugAgents is an independent, self-directed project.*
