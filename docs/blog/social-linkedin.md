# LinkedIn Posts

Four posts for the series. Each is self-contained — they work standalone and also
build on each other if posted in order across a week.

**Posting notes**

| Question | Recommendation |
|---|---|
| Order | Post 2 first if you only post one. "Prompt rules are not guards" is the most transferable lesson and the best performer for an engineering audience. |
| Cadence | One post every 2–3 days. LinkedIn rewards dwell time; four in one day cannibalises reach. |
| Best time | Tue–Thu, 08:30–10:30 IST. |
| Attach | A dashboard screenshot on posts 1 and 3. Document/carousel posts outperform plain text for the launch post. |
| Links | In the post body is fine on LinkedIn (unlike X). Put the primary link in the first comment as well — some audiences read comments first. |
| Comment | Reply to every comment in the first 90 minutes. That window drives most of the distribution. |
| Hashtags | 3–5, at the end. Never inline. |

---

## Post 1 — Series launch

**What I built, and the thing I actually learned**

I spent the last few months building three autonomous agent systems, and then
spending far more time trying to prove they were lying to me.

That second part turned out to be the whole project.

**JobAgents** — a job-search pipeline that sources 7,549 roles from 10 public
APIs, scores every one deterministically, and generates a tailored resume per
shortlisted role. 22,647 scores, zero model calls.

**AgentSwarm** — 34 runs of a multi-agent research arena, where every turn is
recorded in a hash-chained ledger stored *outside* the agents' writable
directory. The audited cannot edit the audit.

**BugAgents** — two agents hunting real vulnerabilities in live bug bounty
programs, behind a gate that only promotes a report when the workspace
corroborates it.

All three are live and publish their own numbers.

Here is what surprised me: in all three, the interesting engineering was never
getting the model to produce output. It was building the component that decides
whether to believe the output.

Every one of these projects is mostly verification code. The model was the easy
part.

I have written the whole thing up — architecture, the bugs, what the agents
actually discovered, and what the results do *not* prove.

Live sites: job.kprsnt.in · agent.kprsnt.in · bug.kprsnt.in

#AIagents #LLM #SoftwareEngineering #MachineLearning #BuildInPublic

---

## Post 2 — Prompt rules are not guards

**A model wrote a resume for me claiming my personal side projects were work I did
for my employer. The prompt explicitly forbade it.**

I had built a resume-tailoring service. The prompt carried the candidate's ground
truth and a clear structural rule: this person has two employers, and everything
else — the independent projects — is self-directed work. Never list a project as
a bullet under an employer.

The model did it anyway. It attributed four separate projects to my employer as
employment history.

I only caught it because I was reading the output line by line.

**The fix was not a better prompt.**

It was about forty lines of code that walks the generated Markdown, tracks which
employer section it is currently inside, and rejects the output outright if a
project name appears as a bullet under an employer heading.

The resume never gets written. No human has to notice.

Then I did the thing that actually matters: I tested the guard against itself. I
seeded eight deliberate fabrications — a fake employer, an invented "847%"
improvement, a fabricated job title, a made-up user count. All eight were caught.

A checker that only ever returns "pass" is worthless. It manufactures confidence
in a verdict nobody verified. You have to try to falsify it before you can trust
it.

**The lesson:** a prompt is a request. If a rule matters, it belongs in code that
can reject the output.

#AIEngineering #LLM #SoftwareEngineering #Agents

---

## Post 3 — Every error was in the prose, not the code

**I had every quantitative claim from a multi-agent research run independently
recomputed. 22 of 25 were correct. Every single error was in the prose.**

I expected the opposite failure mode.

The usual story about LLM output is fluent language sitting on top of broken
arithmetic — confident sentences, wrong numbers underneath. So I built the audit
expecting to find bad computation.

What I found: **zero errors in the Python modules.** Every module computes
correctly.

All five defects were in the markdown reports — introduced when the agents
transcribed their own results into narrative:

- The same mass ratio quoted three different ways across three files, all three
  wrong and mutually inconsistent
- A factor-of-2 slip where a one-way travel time was recorded as half the round
  trip
- Two genuinely different physical quantities sharing one name, never reconciled

The computational reasoning was sound. The transcription was not.

That is a much more tractable problem than "the model cannot do maths." It points
at a specific fix: treat numbers in generated prose as claims to be checked
against the artifacts they came from, rather than as results to be trusted.

The overall verdict was B+ — explicitly *not* publication-grade without that
audit. I am keeping that caveat attached to the work.

**The lesson:** audit the prose, not just the code. The transcription step is
where correct computation goes to die.

#MachineLearning #AIResearch #LLM #DataScience #Agents

---

## Post 4 — Exit code 0 is not evidence of correctness

**The bug that cost me the most time produced no error, no output, and no exit
code. Just silence.**

I was orchestrating several agent CLIs as subprocesses. Spawning one with piped
stdio made it emit zero bytes and never exit. Not a crash. Not a timeout. It just
sat there.

The identical command with output redirected to a file exited 0 in five seconds
with a complete event stream.

That one took me a while, because every instinct says a hang is a problem with
the thing being run. It was a problem with how I was capturing it.

It was not the only one:

**Double-counted output.** I concatenated both the streaming deltas and the final
message content, which duplicated every turn's text. I noticed when I read
`"oneoneUnderstoodUnderstoodOKOK"`. This class of bug never crashes — it quietly
makes every downstream metric wrong.

**A false accusation.** A filename regex that did not allow internal dots
truncated `relativity_calculator.py` to `relativity_calculator`. The file
existence check then failed, and my verifier reported a phantom-artifact
violation — against honest work. My own tooling was generating false positives
about the agents.

**My own contamination.** I wrote a probe file inside the directory the agents
worked in, and deleted it later. The ledger recorded a file-deletion event —
indistinguishable from an agent destroying evidence. The researcher's files
contaminate the measurement.

**The lesson:** these all failed silently. The run reported success while
producing nothing usable. If your verification only checks that a process exited
zero, you are not verifying anything.

Check the output. Every time.

#SoftwareEngineering #Python #LLM #AIEngineering #Debugging
