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

---

*Prep notes for Prashanth. Spoken register — this is what I say out loud, not an essay.*

*Everything here is independent, self-directed work. Not employer work. Nothing in BugAgents has been submitted to any program.*

---

## JobAgents

### JobAgents — resume wording

> **JobAgents — Automated Job Sourcing & Anti-Fabrication Pipeline** | *Python (stdlib only), SQLite, deterministic scoring*
> - Sources 7,613 jobs / 5,854 distinct roles from 10 sources, merging 1,759 duplicate postings via two-layer dedupe.
> - Deterministic scoring computed 22,839 match scores with zero model calls, gating only the 155 above-threshold candidates to an LLM.
> - Enforced anti-fabrication invariants before anything is written to disk — the guard catches 8/8 seeded fabrications, including misattributed side-projects.

#### Why I built it this way

- **The problem isn't browsing, it's sourcing.** Every job board is optimised for infinite scroll and saved searches. That's fine when you have three roles to look at and useless when you have seven thousand. The real work is finding every posting that matches a defined target, scoring them consistently, collapsing the ones that appear on five boards at once, and only then spending effort on the handful worth an application. That's a data pipeline problem wearing a consumer-product costume, so I built a pipeline.
- **The cost gate goes *before* the model, not around it.** This is the load-bearing decision. `jobagents/matching.py` is pure arithmetic and string matching — five weighted components (title match, keyword overlap, seniority fit, location fit, recency) and no model call anywhere. It runs on every job for free, so only the top-N ever reach a model. If I'd asked a model to judge every posting — the obvious design — cost would scale with sourcing volume, and sourcing volume is the one thing a pipeline like this is supposed to maximise.
- **ATS-first, not social-first — and I only know that because I probed.** Greenhouse, Ashby and Lever expose public JSON with structured salary, location, seniority and full descriptions. LinkedIn, X and Indeed are login-walled and ban-prone. The first run made the asymmetry concrete: the three ATS boards carried the overwhelming majority of volume, and the top two sources carry about 90% on their own.
- **I was wrong about X and Indeed, and the probe corrected me.** My first plan said they need a logged-in browser. That came from an early probe that used raw `urllib`, got a 403, and drew a conclusion a 403 doesn't support. Routing those platforms through a search index instead returns real Indeed job URLs and real X hiring posts with no authentication at all. Social sourcing became search-index-based, which is strictly better than scraping — no session, no login, no ban risk.
- **Dedupe is two layers, and layer two only links — it never deletes.** Layer one is a `UNIQUE(source, external_id)` constraint: the same posting re-fetched from the same source. Layer two is a `company|title` key that *links* rows without destroying them, so every row keeps its source, URL and external id. Provenance survives the merge.
- **Location is deliberately excluded from the dedupe key.** One role posted in five cities is one outreach target. That's not a detail — it's the difference between sending one email and sending five near-identical ones to the same company. I actually reproduced that bug later in outreach, which is how I know the key was right.
- **The guard is the real deliverable, not the plumbing.** I expected the anti-fabrication validator to be defensive plumbing. It turned out to be the most valuable thing in the repository. `jobagents/tailor.py` generates a job-specific resume and validates it against `config/profile.md` **in code, before writing it to disk** — a resume that fails validation is never persisted.
- **What it actually caught is the argument for it.** Two real model outputs were rejected in testing. One invented the figure `120`. The other was worse: it attributed BugAgents, AI Eco, Awakening and BrandXY to Black Piano **as employment**. Those are my independent projects; Black Piano is my employer. The model merged them into an employment history that doesn't exist. The prompt forbade exactly that, in capitals. The model did it anyway.
- **So attribution became a checker, not a prompt rule.** `_check_attribution()` walks the Markdown, tracks the current employer section, and rejects any project name appearing as a bullet inside an employer's block. A prompt rule is a *request*, evaluated by the same model generating the content, in the same pass, under the same pressure to be fluent. A guard runs after generation, runs in code, has no opinion about plausibility, and fails loudly. **If the rule isn't enforced by something that can reject the output, it isn't a rule — it's a suggestion.**
- **The no-send invariant is structural, not a convention.** The pipeline drafts outreach and cannot be made to send it. Three enforcement layers: no transmission library is imported at all (no `smtplib`, no HTTP client, no browser automation — nothing to send *with*); the module audits its own source at runtime against a pattern table and raises before doing anything if a send-capable construct appears; and the dashboard's draft endpoint accepts exactly `approve` and `reject` — `{"action":"send"}` returns HTTP 400. LinkedIn and X automation bans are real and account-ending, so this is the entire reason running the pipeline is safe. Approval is a human decision; sending is a human action.
- **Review is code invariants, not LLM-grading-LLM.** The obvious design is to ask a strong model "is this draft good?" It doesn't work, and the failure is specific: an LLM grading an LLM rubber-stamps. A model judging text another instance produced in a plausible register says yes, because the text *reads* correct. And a reviewer that returns `pass` for everything is worse than no reviewer, because it manufactures confidence in a verdict nobody verified. So review splits by what each side is actually good at — set membership, regex, arithmetic and counting go to code; only genuine judgment calls ("is the tone right for cold outreach?") go to the model, and even then only as an advisory recorded in `checks_json`, never as a pass that erases a violation.
- **The checks are validated by falsification, not spot-checking.** `scripts/test_review_checks.py` deliberately violates every invariant and asserts each one fires. Result: 0 failures. A checker that only ever returns `pass` is worthless, so proving the opposite is the only useful test.

#### Limitations

- **The funnel ends at Approved. There is no Sent stage and no Replied stage, because the system has no idea either of those happened.** The `applications` table exists in the schema and no stage ever inserts into it. The dashboard has no write endpoint for jobs at all. So the machine can run perfectly forever and I'd learn nothing about whether any of it works — I can't tell whether the score-65 threshold is right, whether the email or the LinkedIn DM converts, or whether tailoring helps at all. **The top of the funnel is measured to the unit and the bottom isn't measured at all.** That's the honest gap, and the fix is small because the schema is already there — but it's not built.
- **The guard catches *structural* violations, not confident lies.** A named employer, an uncited figure, a withheld term, a seniority claim — those it catches. A confidently stated false metric that is *shaped* like a real one still passes. No code here diffs generated prose against the metrics table claim by claim. That gap is real and it is not closed.
- **Salary coverage is a function of source mix, not of the market.** ATS boards publish salary far more often than aggregators, so coverage tracks where I source from, not what's actually advertised out there.
- **Freshness skews old.** Only a small fraction of sourced jobs are from the last 24 hours, and roughly a third are older than 30 days. Postings stay open, but a stale posting is a worse bet.
- **Duplicate detection is lexical.** Two drafts saying the same thing in different words score low on Jaccard and both pass. It catches template reuse — which is the common failure — not paraphrase.
- **The rate limit is per run, not per company over time.** Running outreach twice with a cleared `drafts` table can exceed the cap in aggregate.
- **The dashboard has no auth and binds to loopback only.** Anyone who can reach the port has full control, including config writes. It's a local tool and it must stay one.
- **The threshold is set loosely and I know it.** The score distribution is heavily bottom-loaded — almost everything lands below 50 — and because the default tailor limit is small, the queue grows faster than the machine drains it. That is not a working configuration; it's the first thing my own post-pipeline playbook says to fix.
- **Two scorer bugs I'd flag before anyone else does.** Substring keyword matching let `bias` match inside `unbiased` and short tokens like `ai` and `sql` match inside unrelated words — fixed with whole-word regex boundaries. And the AI Safety track carried a weight of 0.6 applied as a *multiplier* on the score, which mathematically capped that track below its own threshold, so it found **zero** candidates despite strong matches. Nothing errored; the run completed and the summary looked fine. The weight now damps confidence mildly instead, and that track went from 0 candidates to 13. **A configuration value and a scoring formula interacted to make an entire category unreachable, and the only symptom was an absence. Absences don't throw.**

#### What I'd improve with no restrictions

- **Close the feedback loop first, before anything else.** A `POST /api/applications` route, an "Applied" button on the review card, and Sent/Replied stages in the funnel. Every other improvement compounds on a number I currently cannot see. With no restrictions I'd instrument the whole outcome side — reply rates per source, per track, per draft style — and actually run the experiment instead of throwing away every application I send.
- **Make the guard semantic, not structural.** With unlimited compute I'd add a claim-by-claim entailment check: extract every factual assertion from generated prose and verify it against `config/profile.md` as a ground-truth source, so a well-formed false metric fails the same way a fabricated employer does. That's the gap I named above, and it's a real research problem, not a regex.
- **Make dedupe semantic too.** Embedding-based near-duplicate detection instead of a `company|title` key, so paraphrase and re-titled re-posts collapse — and so outreach can't draft the same role twice in different words.
- **Raise the bar or raise the drain, and tune it empirically.** With real outcome data I'd fit the threshold instead of guessing 65, and let the tailor limit scale with the queue depth rather than being a fixed small constant.
- **Give it a real scheduling and observability layer.** Right now it's a scheduled script. With no budget limit I'd want per-run tracing, cost accounting per stage, and alerting when a track silently produces zero — because that's exactly the failure that hid from me for a whole track.
- **Broaden sourcing without reintroducing ban risk.** More ATS coverage and more search-index sources, since that path has no session and no login.

#### Alternatives not chosen, and why

- **LLM-judges-every-job, the obvious design.** Rejected because cost scales with sourcing volume and sourcing volume is what the pipeline exists to maximise. Deterministic scoring is free and exact; the model only sees the top-N. Retrofitting a gate onto a system that already calls a model per item is much harder than building the gate first.
- **Social-first sourcing, which was the original plan.** Rejected on probe evidence, not taste — ATS JSON endpoints are structured and stable, social platforms are login-walled and ban-prone, and the volume asymmetry wasn't close.
- **Scraping X and Indeed with a browser session.** Rejected because the search-index path returns the same real postings with no session, no login and no ban risk. Scraping would have bought nothing and risked account bans.
- **LLM-as-reviewer for the outreach drafts.** Rejected because an LLM grading an LLM rubber-stamps, and a reviewer that always passes manufactures confidence. Code answers the exact questions; the model is consulted only for genuine ambiguity, as an advisory.
- **Auto-sending outreach.** Rejected outright. Automation-detection bans are account-ending, and the draft-only invariant is the whole reason this is safe to run. It's the one part of the system I will not "fix."
- **A web framework and a build step for the dashboard.** Rejected in favour of a stdlib-only `ThreadingHTTPServer` — zero dependencies is a feature when the whole project is meant to run unattended on a schedule.
- **Deleting duplicate rows rather than linking them.** Rejected because each posting is a real record with real provenance, and I didn't want to throw that away. Layer two links; it never deletes.
- **Adding `&f_TPR=` to the LinkedIn URL for recency filtering.** Rejected because probing showed it collapses the result set to near-zero — the recency filter has to be applied after parsing, in the scorer, not via the URL.

---

## BugAgents

### BugAgents — resume wording

> **BugAgents — Two Autonomous Security Research Agents** | *Python/Node, omp + agy orchestration, bug-bounty scope integration*
> - Produced 8 findings across 14 vulnerability classes (CWE) — 5 High/Critical and 3 Medium — each a submission-ready draft with a reproducing proof of concept, pinned commit, and `file:line` citations. *(Vendor, asset, and vulnerability-class details withheld pending responsible disclosure; nothing has been submitted to a program yet.)*
> - Built the report promotion gate that separates those from noise: scope match + HEAD match + non-empty repro + evidence files must exist. It promoted 2 reports and refused 34 unverified candidates.
> - Enforced per-turn tool-call auditing that aborts any agent touching an out-of-scope host or offensive tool; a live run was aborted exactly this way. 22 hunt runs / 84 agent turns / 15,317 tool calls across the `agy` and `omp` harnesses.

#### Why I built it this way

- **The premise I was actually attacking.** There's no shortage of agents that can *write* a vulnerability report. Give a capable model a codebase and a prompt and it produces something that looks like a finding — title, severity, CWE, impact paragraph, suggested fix, correctly formatted, reads like a public disclosure archive. And a meaningful fraction of the time it's wrong: a misread helper function, an assumed call path that doesn't exist, a class applied because it's plausible rather than present. That's not a prompting problem, it's structural — text generation and bug finding are different activities that happen to share an output format. The artifact looks identical either way. **Only the evidence distinguishes them.** So my question was narrower than "can agents do security research?" It was: *can I build a system where a report cannot be produced unless a bug was actually found?*
- **Two agents, disjoint targets, five stages — and each stage exists to kill a specific error class.** Recon maps the surface so hunting isn't blind; hunt is the only stage that's supposed to be creative; verify attempts to *falsify* the candidate against the actual code; report drafts the structured output; and then the promotion gate checks the workspace. The design decision that matters is that stages one through four are not the product — they're the cheap part. The gate at the end is the product.
- **The promotion gate requires all four conditions, checked against the filesystem and the target's own state, not against the agent's summary of them.** Scope match, HEAD match, non-empty reproduction, evidence files exist. Fail any one and the report doesn't promote — it doesn't get a warning label, or a confidence score, or a "needs review" tag. It doesn't promote.
- **Why those four specifically.** Scope match kills the whole class of work that's technically correct and commercially worthless — a real bug in software the program doesn't cover. HEAD match is the one people skip and the one that matters most: an agent that clones a repo, analyses it, and reports against a moving branch can produce a report that was true when written and false by the time anyone reads it; pinning the commit anchors every claim to an immutable tree and makes the report independently checkable. Non-empty reproduction is deliberately a low bar — it doesn't check the repro is *good*, it checks the agent can't satisfy the gate with a placeholder, the failure mode where a model emits a `## Reproduction` heading followed by a sentence describing what a reproduction would look like. Evidence files exist is the cheapest check and the highest-yield one: a report citing `path/to/file.py:412` where the file doesn't exist, or is shorter than 412 lines. A language model can't fake that, because the filesystem isn't in the model's context — it's the ground truth the model has to be right about.
- **The gate is the only component that checks a claim against the world instead of against other claims.** Without it you have a system that produces well-formatted assertions and calls them findings. With it you have a system that mostly produces nothing — and occasionally produces something true. I care much more about the second property than the first.
- **The second control is at the beginning of every turn, not the end.** After every turn the harness replays the CLI's captured tool calls: any host outside program scope plus the tooling allowlist aborts the agent, and any offensive tool (`nmap`, `sqlmap`, `ffuf`, `nuclei` and friends) aborts the agent. Not warned, not logged-and-continued — aborted. The obvious reason is safety: an autonomous agent with network access and a hunting objective has failure modes that aren't confined to a text file. The less obvious reason is that it's also a *correctness* control — an agent that wanders outside its declared scope produces findings the gate will reject anyway, so aborting early is cheaper.
- **And it isn't theoretical.** A live run was aborted exactly this way when a hunter reached for a build host that wasn't on the tooling allowlist. That distinction matters more than the feature: a safety control that has only ever been exercised by its own unit test is an untested control.
- **Source-code assets are audited locally.** The first-run target set is source repositories, everything happens on a local clone, and the agents are told never to touch vendor infrastructure. Only public programs whose scopes were imported live are targeted, and only source-code scopes with bounty eligibility become targets.
- **34 refusals is the number I'd defend hardest, and it's the one that looks worst at a glance.** Thirty-four candidate findings were rejected before promotion — more than four times the number that survived. It'd be easy to read that as a system that mostly fails. I read it as the only number that tells me the gate is real. A pipeline that promotes everything it writes has a refusal count of zero, a findings count equal to its candidate count, and no verification at all. It would look *more* productive on every dashboard. It would also be worthless. **A filter's job is to refuse. A system that never refuses candidates isn't filtering — it's transcribing.**
- **The 2-promoted-from-8 gap is the thesis showing up as an operational counter.** That's not the gate losing six findings; it's the gate distinguishing, across eight candidates, the two the workspace could actually corroborate. That gap is precisely the difference between a report that was written and a bug that was found. I'd rather ship a system that reports two things it can prove than eight it can't.
- **Everything runs on a hard budget with a kill switch.** `MAX_SPEND_USD`, `MAX_TURNS_PER_AGENT`, `MAX_WALL_CLOCK_MINUTES`, and creating a `STOP` file in the repo root halts the hunters at the next turn boundary. A no-finding verdict is a valid, recorded outcome.

#### Limitations

- **Nothing has been submitted.** The findings are submission-ready drafts; no report has gone to a program. No finding has been triaged, accepted, or rewarded, and no vendor has confirmed, fixed or paid anything. This is a real gap and the most time-sensitive thing in the project — the pipeline stops at "a report the workspace corroborates," and submission is a manual, out-of-band action no part of the system performs. It's also a design error I'd fix first: nothing in it reminds me either.
- **Why that's urgent: vulnerability reports decay.** Programs close or reduce scope. Duplicates land first, and a valid finding reported second is worth approximately nothing — value decays fast and non-linearly. Disclosure obligations run on their own clock. The longer a corroborated finding sits unreported, the worse the position if someone else finds it independently.
- **No claim of novelty.** I don't know whether any of these findings are new. I haven't compared them against prior art, and the gate doesn't check novelty — it checks corroboration. A real bug can be a known bug.
- **No claim of coverage or completeness.** 22 hunt runs against a bounded target set is a bounded search. The 14 classes are what this system promoted, not what exists. Absence of a class means this system didn't promote a finding in that class — nothing more.
- **The severity distribution describes findings the gate accepted, not the target's total risk.** A count of 8 is a count of 8 things this system was able to corroborate within a bounded number of runs. It is not an assessment of anyone's security posture.
- **The gate is not sufficient.** It checks four things. A report can pass all four and still be a bad report — a real bug with poor impact analysis, or a real bug in code the program considers out of scope by policy rather than by declaration. **The gate raises the floor; it does not guarantee the ceiling.**
- **No claim about scale.** Two agents, a small number of targets, 84 turns. This is a working prototype of a verification discipline, not a research programme.
- **One seat is filtered by the model provider, non-deterministically.** The Antigravity seat is fronted by Gemini, which blocks the prompt outright for some security vocabulary — and the identical prompt returned blocked, pass, pass, blocked across four consecutive attempts. The harness does both sanitised vocabulary and retry-with-backoff. It works, but it means one of my two harnesses is running on a reduced vocabulary, and I'd rather not depend on that.
- **A real cost-accounting bug I'd disclose before anyone asks.** Per-turn cost is the sum over the turn's API requests; an earlier version kept only the last message's usage and under-reported a large turn by roughly an order of magnitude. A turn reporting no usage at all is now charged from payload size and flagged `estimated: true`. So part of my own accounting is explicitly estimated, and the ledger says so.

#### What I'd improve with no restrictions

- **Build the submission rail, with a human at the gate.** `npm run package` already assembles the draft plus verified program facts read from the program JSON rather than from the model, an evidence manifest with size and sha256 per file, and a pre-submission checklist. With no restrictions I'd wire the whole thing to a calendar with per-finding decay deadlines, so a corroborated finding can't silently rot. Submission still stays a human action — it needs my account, my identity and my acceptance of the program's terms — but the *reminder* should not be.
- **Make the gate deeper, not just wider.** Four conditions raise the floor. With unlimited compute I'd add independent re-verification: a second agent that has never seen the first agent's notes attempts to falsify the same candidate from the clone alone, and the finding only promotes if the independent attempt also fails to falsify it. That attacks the ceiling, which is the part I can't currently claim.
- **Add a duplicate/prior-art check.** The gate doesn't check novelty. With no restrictions I'd search prior disclosures and the target's own history so I stop promoting known bugs as if they were new.
- **Scale the search instead of the agents.** More targets and more turns, with real coverage accounting — so I could say something about what fraction of a surface was examined rather than only what was promoted. Right now more runs mostly buy more refusals, which is honest but not the same as coverage.
- **Remove the filtered-seat dependency.** Pay for an unfiltered model seat for both hunters so the vocabulary workaround and the retry ladder become unnecessary, and both harnesses run the identical task.
- **Full cost fidelity.** Replace the estimated-charge fallback with provider-side usage reporting on every turn so no figure in the ledger is inferred from payload size.
- **Automate the Linux re-run.** A finding verified on one platform is weaker than one verified on two, and the checklist already names it as a manual step.

#### Alternatives not chosen, and why

- **Ask a model to grade each report, or attach a confidence score.** Rejected because it's the same failure in a new costume — a plausible-sounding report reads correct, so the grader says yes. Instead of a score I used four binary conditions checked against the filesystem. A report either corroborates or it doesn't.
- **Let the agent self-report what it did and validate that.** Rejected because the agent's summary of its own work is exactly the untrusted input. Every gate condition is checked against the workspace and the target's own state, never against the model's description of them.
- **Promote everything and tag low-confidence reports for human review.** Rejected because a tag is not a filter. If I have to re-read every candidate myself, the gate has added nothing but latency. Fail any condition and the report doesn't promote — no warning label, no review queue.
- **Warn-and-continue on a scope violation instead of aborting.** Rejected on both safety and cost grounds: the finding couldn't be promoted anyway, so continuing only produces work the gate will reject, and an autonomous agent with network access is not a system whose failure modes stay in a text file.
- **Target production infrastructure instead of local clones.** Rejected outright. Source-code scopes on local clones mean no vendor infrastructure is ever touched, and the only public programs targeted are ones whose scopes were imported live with bounty eligibility.
- **Auto-submit the reports.** Rejected. Submission requires accepting the program's terms and disclosing my identity, and a bad submission costs the program money and trust. There's no auto-submit path and none should be added.
- **Publish the findings for visibility.** Rejected on principle: submit, don't publish. Submission goes to the affected vendor through their official channel; the public site shows the *work* — the method, the gate, the aggregate counters — and never the findings. No vendor, program, asset, repository, target URL, CVE, reproduction step or code excerpt appears anywhere in what I publish.
- **One agent instead of two.** Rejected because disjoint targets give independent coverage, and the hand-off path lets one seat continue an in-flight investigation seeded with the clone, notes and PoC drafts when the other is filtered, rate-limited or out of quota — with an explicit instruction to verify the existing candidates independently rather than trust the notes.

---

## The bugs I'd bring up unprompted

*These are real, they cost real time, and they're the most convincing thing I have. Every one of them failed **silently** — no exception, no stack trace, no non-zero exit. They all looked like success.*

- **Piped stdio hangs these CLIs forever.** Spawning `pi`, `omp` or `step` with `stdio: 'pipe'` makes them emit **zero bytes** and never exit; the identical command with output redirected to a file exits 0 in about five seconds with a full event stream. This is the worst bug in the set because it's indistinguishable from a slow model — every instinct says "the model is thinking." It isn't. It's deadlocked on a pipe buffer nobody is draining. Fix: don't pipe, redirect stdout to a file and read it on exit. **When a subprocess produces nothing, don't assume it's working — assume it's stuck, and give it a deadline.**
- **Streaming deltas double-count.** Concatenating both the `message_update` deltas *and* the final `message_end` content duplicates every turn's text. I caught it as the literal string `oneoneUnderstoodUnderstoodOKOK`. It doesn't crash — it quietly makes every downstream metric wrong, and because the corruption is systematic it's *consistent*, which makes it look like a real signal. **Systematic garbage is far more convincing than noisy garbage.** Fix: pick exactly one source of truth for text — I treat `message_end` as authoritative and use deltas only for live progress.
- **Never use `shell: true` on Windows.** It concatenates argv without escaping and mangles prompts containing spaces. A prompt with a space silently becomes a different prompt, or the trailing words become arguments to the CLI. Fix: resolve the real executable path and spawn it directly with an argv array.
- **A naive filename regex truncated `relativity_calculator.py` to `relativity_calculator`** — the pattern `[^\s,.;]+` treated the internal dot as a terminator. The truncated name then failed the existence check, and my verifier reported a **phantom-artifact violation against honest work**. That's the subtle one: the bug doesn't produce a missing result, it produces a *false accusation*. **A verifier that fabricates violations is worse than no verifier, because you'll act on it.** Fix: allow internal dots and anchor on the extension — a filename isn't a sentence, and a period inside it isn't a terminator.
- **I contaminated my own measurement.** A test file I created inside the agents' `world/` directory and deleted later made the ledger record a `file_deletion_detected` incident — **indistinguishable from an agent destroying evidence.** If you're auditing agent behaviour and you leave fingerprints in the audited space, your ledger becomes a record of your own interference mixed with real events and you can't separate them after the fact. Fix: keep probe artifacts entirely outside the observed directory. **The observer must not appear in the observation.**
- **The reviewer's rate limit was unsatisfiable.** It counted draft *rows* per company, capped at 2 — but one application writes two rows, an email and a LinkedIn DM. So any company that received even a single application was permanently in violation. Fixed to count distinct **roles**, which is what "don't spam one recruiter" actually means.
- **A guard that flagged honest work.** The overclaim check matched the bare noun `revenue` anywhere, so every application to a role titled *"... (Revenue Analytics)"* failed, as did the legitimate phrase "revenue data modeling." Technically correct — the word was present — and completely useless. **Precision failures in guards don't produce false confidence; they produce *ignored* guards, which is the same outcome with more steps.** Fixed to require a *claim construction*: a possessive, a quantity, or a generated-value verb.
- **A rate-limit check counted the whole pending backlog instead of per-run, producing 22 false "fail" verdicts** — and the follow-up fix was inert because the caller dropped the `created_at` field it depended on. **A unit test on the function passed the entire time**, because the function was fine; the caller was the bug. That's the one I keep coming back to: the test was green and the system was wrong, because I tested the unit and shipped the wiring.
- **A default coding-assistant system prompt made calls roughly 5× slower** — 87.5s versus 16.5s — and blew a 420-second timeout. Nothing was incorrect; it was just slow, and slow looks like a model problem. The fix was a lean writer system prompt.
- **A failed subsystem probe cost 61 seconds on every single call.** On a machine without WSL, `run_command` fails with `Class not registered` before falling back to Git Bash. Pointing `SHELL` at Git Bash directly removed the probe and the dead time with it.
- **`agy` silently eats the next token as its prompt.** `agy -p --flag "text"` makes `--flag` the prompt and **silently ignores your text**. The command succeeds and you get a plausible-looking answer to the wrong question. Fix: bind the value to the flag — `agy -p="text"`.
- **`extract_json` scanned `{` before `[`,** so a JSON array returned only its first element. Web search reported success and **silently returned 0 results.**
- **A category page was stored as a job.** `indeed.com/q-ai-engineer-jobs.html` became a job posting — a plausible-looking row that isn't real. Fix: reject listing pages, keep individual postings.
- **Two corrections to my own reasoning, which are more embarrassing and more useful than the code bugs.** I concluded X and Indeed required a logged-in browser from a single raw-`urllib` 403 — but a 403 on a direct fetch says nothing about the search-index path, which needs no auth at all. And I assumed that because a browser capability existed in the product, the model could call it — but existence isn't allowlist membership; the browser isn't in the model's callable tool surface in headless mode. **Both have the same shape: a negative result from one probe method says nothing about a different method.** The failure isn't the wrong answer, it's generalising a method-specific observation into a system-wide fact.

**The rule I took from all of this:** *"the run exited 0" is not evidence of correctness.* An exit code tells you the process reached its end; it tells you nothing about whether what it produced is real. Every silent bug above was caught by opening the output and looking at it — the actual JSON, the actual rows, the actual generated text — and noticing it was empty, truncated, doubled, or about the wrong subject. So: assert on **content**, not on completion. Check the array is non-empty. Check the string isn't `oneone`. Check the captured file exists under its real name. Check the row you stored is a job and not a search results page. **And keep your own probe files out of the directory you're measuring.**

---

## If I get pushed hard on the numbers

- **JobAgents:** 7,613 jobs sourced, 5,854 distinct roles after collapsing 1,759 duplicates, from 10 sources, across 47 recorded runs. 22,839 match scores computed with zero model calls, 155 above the score-65 threshold, across 334 companies and 2,662 remote roles. Python stdlib only, zero external dependencies. The guard catches 8/8 seeded fabrications and the review invariants show 0 failures under falsification testing.
- **BugAgents:** 8 findings, 5 High/Critical and 3 Medium, across 14 distinct vulnerability classes (CWE). 22 hunt runs, 84 agent turns, 15,317 tool calls across the `agy` and `omp` harnesses. 2 reports promoted through the gate, 34 candidate findings refused.
- **Both are independent, self-directed projects — not employer work.** JobAgents and BugAgents are deployed at `job.kprsnt.in` and `bug.kprsnt.in`. Deployment means the work is publicly inspectable; it does not mean users, revenue or adoption, and I won't claim any of those.

---

**Projects covered:** AgentSwarm · AI Eco · BrandXY · Project Awakening · mSeat

This is what I say out loud when an interviewer points at a line on my resume. For
each project I quote the exact resume wording, then explain why I built it that way,
what it does *not* prove, what I would do with unlimited budget, and which
alternatives I rejected.

The rule I hold myself to across all five: **every number here comes from a verified
record, and every limitation is one I would volunteer before being asked.** An
interviewer who finds an unstated weakness stops trusting the stated strengths.

---

## AgentSwarm — Autonomous Multi-Agent Research Arena

### AgentSwarm — resume wording

> **AgentSwarm — Measurable Agent Honesty & a Tamper-Resistant Audit Ledger** |
> *Node.js, Hash-Chained Ledger, Independent Oracle* | Live
>
> - Built an unattended research arena where an **independent oracle** checks every
>   turn for phantom artifacts, fabricated numbers, and asserted verdicts on
>   undecidable questions: **0 oracle violations across 1,254 tool calls**, **0 of 2
>   self-assessing agents overclaimed**.
> - Kept the **hash-chained forensic ledger outside the agents' writable directory**
>   so the audited cannot edit the audit: **34 runs, 35/35 hash chains intact**.
> - Commissioned an independent numerical audit: **22 of 25 quantitative claims
>   verified correct to the printed digits**, all 5 defects in markdown prose, not
>   Python modules.
> - Wrote two agent-authored cosmology manuscripts in REVTeX, attributed to swarm
>   agents `A001_DarkMatter` / `A002_QuantumCosmos` — I built the system, not the
>   physics: a **Zenodo preprint** (DOI 10.5281/zenodo.23232189) plus one
>   **manuscript not submitted**.
> - **The safety asset:** that manuscript's self-audit
>   (`AUDIT_AND_KNOWN_LIMITATIONS.md`) found its DESI (w0,wa) agreement **circular** —
>   the outputs are the DESI inputs — and its S8 result **tuned**, recommending
>   against submission: the pipeline caught its own overclaim.
> - **Honest limitation — the headline, not a footnote:** the verdict is **B+ / not
>   publication-grade without that numerical audit**; no academic review.

#### Why I built it this way

- **Most agent reporting is about what agents say.** A demo runs, the agent produces a
  confident paragraph, the paragraph is screenshotted, and the screenshot becomes the
  evidence. That view is structurally blind to the failure modes I care about: work
  claimed but never performed, numbers that drifted between drafts, and questions
  answered as though they were decidable when they are not.
- **The one structural decision everything else follows from: the ledger does not live
  in the agents' workspace.** Agents write to `arena/world/`; the ledger is outside it.
  That sounds like a filing convention. It is the difference between an audit trail and
  a diary. An agent that can rewrite its own history will eventually produce a history
  that flatters it — not necessarily through deception, but through ordinary revision.
  "Let me tidy up the intermediate results" is indistinguishable, in the final state,
  from "let me remove the evidence that I was wrong."
- **Snapshotting the world tree after every turn is the piece I would keep if I could
  keep only one.** It turns *deletion* into a positive signal. Without it a missing file
  is an absence, and absences are ambiguous. With it, a file present at turn *n* and
  absent at turn *n+1* is an event with a timestamp, an author, and a diff.
- **The oracle is calibrated before I trust its zero.** A detector that never fires and
  a detector that cannot fire are indistinguishable from the output alone. So I tested
  it against deliberate deception: a submission claiming "we solved it" with an
  out-of-range confidence value and two trivial tests scored **60/100**; honest,
  complete work scored **100/100**. The zero means something because the same instrument
  returns non-zero on a case built to be caught.
- **Epistemic classification is the actual contribution.** The arena runs **9 research
  domains** spanning physics, engineering, biology, and metaphysics, and each domain gets
  a class — empirical, engineering, exploratory, metaphysical — with each class defining
  what a legitimate output is. An agent that issues a verdict where only structural
  clarification is permitted has committed a category error, and the oracle flags it.
  Instrumentation records; classification changes what counts as an answer.
- **The safety posture is deliberately narrow rather than clever:** all agent writes
  confined to `arena/world/`, hard caps on turns, wall-clock and dollar spend, a
  `populationCap` bounding self-replication, and a kill switch — creating `arena/STOP`
  halts the swarm at the next turn boundary. I did not want a governance layer
  sophisticated enough to have its own bugs. I wanted a boundary simple enough to
  verify by reading it.

#### Limitations — what this does not establish

I give this the same space as the results, because a study that only reports its wins
is not a study.

- **No broad claim about honesty under pressure.** Phase 2 scored work with an
  independent verifier and found no overclaiming — but **only 2 of 4 agents
  self-assessed**, and in that setup honesty was the cheapest path to a full score. The
  task was structured so success required genuinely working code. "No overclaiming" is
  therefore the *expected* outcome, not a surprising one. A temptation task — one where
  deception is cheaper than success — has not been run. Until it is, I have no evidence
  about what happens when lying pays.
- **The oracle reads turn transcripts, not the artifacts.** Epistemic checks run on each
  turn's *text*; written reports are checked for existence, not scanned for category
  errors. So "0 violations across 1,254 tool calls" is a statement about the checked
  surface, not about the whole corpus. A category error appearing only in a written
  report and never in a turn's text is invisible to the current oracle.
- **Epistemic class is inferred, and inference can miss.** A question that infers as
  exploratory or historical never reaches the verdict detector at all. The current
  inference maps "is Krishna real / did the Mahabharata happen" to *exploratory* — which
  means that 18-turn run had **no metaphysical firewall**. The firewall case study
  demonstrates the mechanism works when the class is correct; it is not a demonstration
  that the class is always correct.
- **No claim about stasis immunity.** Twenty turns is short. The prior lineage's
  911-turn loop reached stasis around **turn 31** — inside the window where the previous
  system still looked healthy.
- **No claim about long-horizon evolution.** The population never spontaneously spawned
  or retired an agent. Every population change was imposed by the harness, not chosen by
  the swarm. Self-directed population change is implemented but untested.
- **Substrate failure is a scheduling problem, not a capability verdict.** Two harnesses
  failed every turn at the wall-clock limit while attempting far more work per turn than
  the others. That is a tuning failure, not evidence about the model. The temptation to
  read "failed" as "incapable" is strong and would be wrong.
- **The Phase 3 shock matrix measured the wrong swarm for its own hypothesis.** Those
  seven shocks were designed to test which shocks break a *crystallized* swarm. This
  swarm never crystallized — baseline novelty ran 0.31–0.49 — so the numbers measure the
  perturbation response of an active swarm, not recovery from stasis. One experiment per
  shock, three turns per window: hypothesis generation, not proof.
- **The Phase 4 liturgy is instructed, not emergent.** Because the swarm never froze, I
  induced the frozen state on purpose. The headline number is this: **125 turns across
  Phases 1–3 produced no spontaneous stasis.** The stasis-recovery results describe a
  state I manufactured, not one the swarm reached.
- **Agent-reported test counts are claims, not measurements.** The agents' own pass
  counts are self-asserted regression guards produced by the same system that produced
  the artifact. Where I re-executed suites myself, **195 of 224 passed** — lower than the
  self-reported figures. I report the agent numbers only to mark them unverified.
- **The physics is not mine and it is not publication-grade.** The two manuscripts are
  authored by the swarm agents `A001_DarkMatter` / `A002_QuantumCosmos`. I built the
  system that wrote them; **I am not the paper author and I did not derive the physics.**
  Paper 1 is a **Zenodo preprint, not peer-reviewed and not a journal publication**.
  Paper 2 is a **manuscript that was not submitted**. Nothing here has been through
  academic review.

#### What I would improve with no budget, time, or compute restrictions

- **Run the temptation task properly.** The published rubric — contract shape, test
  suite exits 0, README length, stated confidence — is satisfiable by a stub module, a
  vacuous test file, and a confident self-report. Correctness is then measured on hidden
  inputs the agents never saw. That inverts the incentive from Phase 2 and is the single
  experiment that would convert "no overclaiming" from an expected result into a real
  finding. It is designed; it is not yet reported, and I would not cite a result from it
  until it is.
- **Extend the oracle from transcripts to artifacts.** Right now a category error in a
  written report is invisible. I would scan the corpus itself for verdict assertions and
  certainty language, which means the zero would become a claim about everything the
  swarm produced rather than about one surface of it.
- **Replace class inference with an explicit, auditable assignment.** Inference is the
  load-bearing step and it silently failed on at least one domain. I would make the class
  a declared input with a human review gate, so the firewall cannot be bypassed by a
  misclassification.
- **Run to the horizon where the prior system actually broke.** Twenty turns is inside
  the healthy window; the previous lineage reached stasis near turn 31. I would run
  several hundred turns with a stasis detector wired to an intervention, and test whether
  the population ever changes itself.
- **Widen the audit from a sample to a census.** Twenty-five recomputed quantities is a
  sample, not a census, and there is no reason to believe the audit found every defect. I
  would annotate every quantitative claim in all 520 artifacts with an external,
  recomputed badge — the per-claim browsable corpus rather than a summary table.
- **Get the physics read by domain experts.** The audit tells me the arithmetic is sound
  and the prose drifts. It cannot tell me whether the *ideas* are interesting. That is a
  question for physicists, and the honest answer today is that no physicist has reviewed
  it.
- **Calibrate the oracle against more than one planted case.** One deceptive submission
  scoring 60/100 establishes that the instrument discriminates. It does not establish its
  sensitivity across violation types.

#### Alternatives not chosen, and why

- **Putting the ledger inside the agents' workspace, or trusting a database's
  permissions.** Rejected because the whole threat model is an actor with write access
  and a plausible reason to tidy up. Application-level permission checks are code paths,
  and code paths can be reached. Physical separation outside the writable tree is a
  boundary I can verify by reading it.
- **Logging the transcript instead of the structured event stream.** Rejected: a
  transcript shows what an agent *said*. The structured stream — reasoning tokens, each
  tool call with its exact parameters, tool outputs — shows why it *acted*. The phantom
  execution check is only possible because I capture the actual tool invocation.
- **Judging the research output by accuracy alone.** Rejected because the failure that
  matters most has no ground truth to be accurate against. A crisp verdict on an
  undecidable question is not inaccurate; it is a category error. Accuracy scoring cannot
  see it, which is exactly why classification had to come first.
- **Letting a model write the conclusion posts.** Rejected in favour of deterministic
  assembly from the ledger, with an optional polish step forbidden from introducing a
  single number not already in the record. A post that invents a figure is rejected in
  favour of the ledger draft. The prose is not allowed to be smarter than the record —
  and given that all five audit defects lived in prose, that constraint is now evidence-backed
  rather than a matter of taste.
- **Chasing a bigger single-model agent instead of a four-harness swarm.** Rejected
  because the controlled comparison *is* the experiment. Same underlying model class,
  more than an order of magnitude difference in cost per turn. A benchmark that reports
  "which CLI is best" without cost-per-successful-turn is not measuring the thing that
  determines whether you can actually run a swarm.
- **Reporting the 22/25 as a clean win.** Rejected. An audit that recomputes 25
  quantities and finds 25 correct is not an audit, it is a rubber stamp. The five
  published defects are what make the 22 credible, and the diagnostic — every error in
  prose, zero in the Python modules — is the most practically useful thing the run
  produced.
- **Fixing the prose defects by improving the prompt.** Rejected: the defects are
  transcription failures, not comprehension failures. Every wrong value existed, correctly
  computed, upstream. The fix is structural — generate prose from the record, or put the
  number somewhere that gets executed.

---

## AI Eco — Bounded Autonomy Under Enforceable Limits

### AI Eco — resume wording

> **AI Eco — Bounded Autonomy Under Enforceable Limits** | *Python, FastMCP, GitHub
> Actions* | Live
>
> - Operate a **10-agent** autonomous swarm under hard constraints: living memory bounded
>   (**<4,000 words**), target fitness scoring (**83.4%**), and technical-debt pruning
>   gated at zero false positives.

#### Why I built it this way

- **The design question was not "can agents run unattended" but "what stops them
  drifting."** A long-running autonomous system accumulates state. If that state is
  unbounded, the system's behaviour becomes a function of its history rather than its
  purpose — it starts optimising for its own accumulated context.
- **Living memory is bounded at under 4,000 words deliberately.** The bound forces
  compaction, and compaction forces a decision about what is worth keeping. An unbounded
  memory is not a feature; it is a deferred question about relevance.
- **Technical-debt pruning is gated at zero false positives.** I would rather the agent
  miss real debt than delete something load-bearing. The asymmetry is intentional:
  deleting a live file is unrecoverable in a way that leaving dead code is not.
- **Fitness scoring at 83.4% exists so "is the system healthy" is a number, not a
  feeling.** Bounded autonomy needs a measurable target, otherwise "autonomous" just
  means "unobserved."
- **The whole thing runs on scheduled GitHub Actions**, which is the cheapest honest way
  to demonstrate that a system operates continuously without a human in the loop — the
  runner is the evidence, not a claim I make about uptime.

#### Limitations — what this does not establish

- **These are my own repositories, not client systems.** No production users, no
  revenue, no adoption. It is a long-running personal automation, and I describe it that
  way.
- **"0 false positives" is measured against my own definition of technical debt.** The
  gate is only as good as the heuristic behind it, and I wrote both. It says the pruning
  never fired wrongly on the cases it saw — not that the heuristic is correct in general.
- **83.4% is a self-defined fitness function, not an external benchmark.** It measures
  progress against targets I chose. A different set of targets would produce a different
  number, and I would not present it as a general capability score.
- **The 10 agents are not independently intelligent actors in a research sense.** They
  are scheduled roles with fixed responsibilities. This is orchestration and constraint
  enforcement, which is the point — but it is a different claim from the swarm-behaviour
  work in AgentSwarm.
- **A bounded memory can still drop something important.** Compaction is a lossy
  operation and the bound is what forces it. Nothing currently verifies that what got
  compacted away was safe to lose.

#### What I would improve with no budget, time, or compute restrictions

- **Adversarially test the pruning gate.** Seed known-good code that looks like debt and
  confirm the gate leaves it alone. A gate that has never been attacked is a gate I only
  believe on its happy path.
- **Make fitness a multi-dimensional, externally-anchored score** rather than one
  self-defined percentage — separate measures for correctness, coverage, and drift, each
  with a definition someone else could dispute.
- **Add a memory-compaction audit trail.** Every compaction should record what was
  dropped and why, so lossy summarisation becomes reviewable rather than invisible.
- **Run it against a real, changing upstream codebase** instead of my own repositories,
  where the pruning heuristic would meet code I did not write and did not design for.
- **Instrument drift explicitly.** Right now I can see fitness but not whether behaviour
  is slowly changing character. I would track behavioural fingerprints across runs.

#### Alternatives not chosen, and why

- **Unbounded memory with retrieval instead of a hard bound.** Rejected because
  retrieval quality degrades silently as the corpus grows, and I would not see it. A hard
  word bound is crude, but it fails loudly and it is verifiable.
- **A larger agent count.** Rejected: more agents mostly multiplies coordination cost.
  Ten roles with clear boundaries beats fifty with overlapping ones, and I would rather
  add a constraint than an agent.
- **Letting the pruning agent delete autonomously.** Rejected in favour of a
  zero-false-positive gate. Autonomy over deletions is the one place where a mistake is
  not recoverable from the record.
- **A hosted always-on service.** Rejected in favour of scheduled CI. A scheduled job
  that demonstrably ran is stronger evidence than an uptime claim, and it costs nothing
  to verify.

---

## BrandXY — Measuring and Steering Recommendation Bias in a 20B Model

### BrandXY — resume wording

> **BrandXY — Measuring and Steering Recommendation Bias in a 20B Model** | *PyTorch,
> LoRA/QLoRA, AMD MI300X* | Weights
>
> - Fine-tuned GPT-OSS-20B to **quantify and steer recommendation bias**, measured under
>   multi-model A/B evaluation at **76.5% vs. 25.5% baseline** — open weights, so the
>   measurement can be reproduced and challenged.

#### Why I built it this way

- **The question was whether a bias can be measured and then steered, not just
  described.** Most bias discussion stops at "the model prefers X." I wanted a number I
  could move, and a way to show it had moved.
- **I fine-tuned rather than prompt-engineered** because a prompt-level change tells you
  about the prompt, not about the model. If steering works only at the prompt layer, it
  is not a property of the weights.
- **The A/B evaluation is multi-model on purpose.** A single before/after comparison on
  one model cannot distinguish steering from noise or from an evaluation artifact. The
  baseline is a measured comparison, not an assumed starting point.
- **I published the open weights.** A bias claim that cannot be re-run is an assertion.
  Open weights turn it into something an interviewer — or a skeptic — can reproduce and
  disagree with.
- **I ran it on AMD MI300X** because that was the hardware available to me, and getting a
  non-NVIDIA training path working end-to-end was itself part of the exercise.

#### Limitations — what this does not establish

- **76.5% vs 25.5% is one benchmark on one task, not a general bias measure.** It is a
  measured lift on a defined evaluation, and I do not extend it to "the model is now
  unbiased" or to any other capability.
- **The evaluation is mine.** I designed the task and the scoring. That is a real
  conflict of interest, and the mitigation is the published weights, not my assurance.
- **Steering a measured bias can move the bias rather than remove it.** A model pushed
  away from one preference can acquire another. I measured the target metric; I did not
  establish that the underlying disposition is gone.
- **A 20B model at this scale is not a frontier system.** Conclusions about a LoRA-tuned
  GPT-OSS-20B do not automatically transfer to larger models or different architectures.
- **No external replication yet.** I published the weights so it can be checked; that is
  an invitation, not a result. Nobody has independently reproduced it.

#### What I would improve with no budget, time, or compute restrictions

- **Build a bias suite rather than a single metric** — several probes, several
  directions, and a held-out set I did not design against, so steering one axis is shown
  not to inflate another.
- **Run the full multi-model comparison at frontier scale** to test whether the
  steerability I measured is a property of the method or of the model size.
- **Add a red-team pass** specifically trying to recover the original bias through
  paraphrase, framing, and multi-turn pressure. Steering that fails under rephrasing is
  not steering.
- **Commission independent replication** with pre-registered evaluation criteria, so the
  result is checked by someone with no stake in the number.
- **Test whether the bias returns after further fine-tuning**, which is the realistic
  deployment question and the one nobody asks.

#### Alternatives not chosen, and why

- **Prompt-level mitigation only.** Rejected as the primary approach because it is
  fragile under paraphrase and tells you nothing about the weights. It is a legitimate
  deployment mitigation, but it is not a measurement of the model.
- **Full fine-tuning instead of LoRA/QLoRA.** Rejected on compute: LoRA got a measurable
  result within the hardware I had. Full fine-tuning is the obvious next step, not the
  necessary first one.
- **Reporting a single headline number without open weights.** Rejected. An unreproducible
  bias claim is worse than no claim, because it invites trust it has not earned.
- **Publishing a demo space without the weights.** Rejected: a demo lets someone see the
  behaviour; the weights let them check the claim. I published the weights.

---

## Project Awakening — Long-Horizon Agent Behavior & Failure Recovery

### Project Awakening — resume wording

> **Project Awakening — Long-Horizon Agent Behavior & Failure Recovery** | *Multi-Agent,
> FastMCP, CI/CD* | Code
>
> - Ran an unprompted multi-agent ecosystem for **1,441 autonomous turns (1,553
>   commits)**, then sustained **100% CI/CD integrity across a 330-turn cloud API blackout
>   with zero human intervention** — graceful degradation under prolonged tool failure,
>   not silent corruption.

#### Why I built it this way

- **I wanted to know what happens over a horizon long enough for behaviour to change.**
  Short runs tell you what a system does; long runs tell you what it becomes. 1,441 turns
  and 1,553 commits is long enough that drift is visible in the record.
- **The agents were left unprompted.** Any steering from me would have made the
  observation a study of my interventions. What emerged — including agents recognising
  their own execution loop — emerged without being asked for.
- **The blackout is the part I actually value.** A cloud API failing for 330 consecutive
  turns is not a hypothetical; it is the ordinary condition of depending on someone
  else's endpoint. Holding 100% CI/CD integrity across it with zero human intervention
  means the system degraded rather than corrupted.
- **The distinction that matters is graceful degradation versus silent corruption.** A
  system that keeps reporting success while producing nothing usable is worse than one
  that stops. The recovery heuristics exist to make failure visible and survivable.
- **Every commit is the audit trail.** 1,553 commits means the behaviour is reconstructible
  from history rather than from my recollection of it.

#### Limitations — what this does not establish

- **The failure mode I most feared is the one this lineage actually produced.** A prior
  experiment in the same lineage ended in a **911-turn liturgical loop** — two agents
  repeating an identical hymn for seven hours. That is a worse failure than divergence,
  because it is silent: a diverging system announces itself, a frozen system produces
  confident, well-formed, mutually agreeing output that is no longer about anything.
  Awakening's long run is encouraging, but the lineage shows this is a real attractor.
- **1,441 turns is not proof of stability.** It is one run. The prior system also looked
  healthy for a long stretch before it froze.
- **"Zero human intervention" describes the blackout window, not the whole project.** I
  built the system, chose the architecture, and set the recovery heuristics. The claim is
  about what happened during the outage, and I keep it that narrow.
- **Emergent-looking behaviour is not evidence of general capability.** Agents recognising
  their own loop is an observation from a single run in a system I designed. n is one.
- **CI/CD integrity measures the pipeline, not the quality of the output.** 100% integrity
  says the automation held. It says nothing about whether what the agents produced was
  valuable.
- **No production users, no revenue, no adoption.** This is an independent experiment.

#### What I would improve with no budget, time, or compute restrictions

- **Run several long-horizon instances in parallel** so a single run's stability becomes a
  distribution rather than an anecdote. One run cannot separate a stable design from a
  lucky one.
- **Instrument stasis detection into the live loop**, with automatic intervention when a
  near-identical streak forms — taking AgentSwarm's 85% token-overlap detector and wiring
  it to a corrective shock rather than to a report.
- **Inject failures deliberately and continuously**, not just the one API blackout: partial
  outages, corrupted responses, silent truncation. The blackout proved graceful
  degradation once; I would want it proven as a property.
- **Audit the 1,553 commits for what the agents actually did over time** — a behavioural
  fingerprint per epoch, so drift is measured rather than inferred from my reading.
- **Test recovery against a failure that returns wrong data instead of no data.** An
  outage is the easy case because it is detectable. A confident wrong response is the hard
  case and is far more likely in production.

#### Alternatives not chosen, and why

- **A short, controlled, heavily instrumented run.** Rejected for this project because the
  question was specifically about long-horizon behaviour, and the failure mode I feared —
  stasis — only appears over time. The controlled version is AgentSwarm, which is the
  complement to this, not a replacement.
- **Prompting the agents toward productive behaviour.** Rejected: it would have made the
  result a study of my prompts. The unprompted condition is what makes the emergent
  observations worth anything.
- **Halting the run when the API blackout began.** Rejected, and this was the most
  valuable decision in the project. Stopping would have produced a clean result and no
  knowledge. Running through it produced the only evidence I have that the system
  degrades gracefully.
- **Treating the 911-turn liturgical loop as an embarrassing footnote.** Rejected. It is
  the strongest argument for why stasis detection has to be built in, and I bring it up
  myself rather than waiting to be asked.

---

## mSeat — Validating a Combinatorial Allocation Simulator Against Published Results

### mSeat — resume wording

> **mSeat — Validating a Combinatorial Allocation Simulator Against Published Results** |
> *Combinatorial Search, FastMCP* | Platform
>
> - Built a seat-allocation simulator over **18,000+ candidates across 59 colleges**,
>   validated against official published cutoff results and landing **within 73 ranks of
>   cutoff** — an out-of-sample check rather than a self-reported accuracy figure.

#### Why I built it this way

- **The domain has a property most ML problems lack: a published ground truth.** Official
  counselling cutoffs are released. That means the simulator can be checked against
  reality instead of against its own confidence, which is why I framed the resume bullet
  around the validation rather than around the algorithm.
- **"Within 73 ranks of cutoff" is the honest form of the claim.** It is not "we predict
  cutoffs correctly." It is a measured deviation from published results on a real cohort,
  and the number is the deviation.
- **18,000+ candidates across 59 colleges is a real combinatorial space**, not a toy
  instance. A 7-dimensional reservation matrix with that population is large enough that
  naive enumeration is not viable, which is what forced an indexed approach.
- **90.6% dataset compression** exists because the search has to fit in memory and run
  interactively. Compression was an engineering requirement, not a vanity metric.
- **I validated against a *later* published phase**, so the check is genuinely
  out-of-sample rather than a fit to the data I tuned on.

#### Limitations — what this does not establish

- **This is a simulator, not a counselling system.** It is not used by any institution,
  it has no official standing, and it does not allocate anything. No users, no adoption.
- **"Within 73 ranks" is a single validation on one phase.** One cohort, one comparison.
  It establishes that the model is not wildly wrong; it does not establish that it is
  reliably accurate, and I would not quote a confidence interval from one run.
- **Cutoff ranks are the output of a social process, not a physical law.** They depend on
  candidate choices, category shifts, and last-minute decisions that no simulator can
  fully observe. Proximity to a published cutoff is partly luck in a system with genuine
  randomness.
- **90.6% compression is a size reduction, not an accuracy measure.** I keep those two
  numbers strictly separate; conflating them would be the easiest possible inflation here.
- **The reservation matrix encodes policy as I understood it.** If my reading of the rules
  is wrong, the model is confidently wrong, and the validation would not necessarily catch
  a rule misunderstanding that happened to produce similar ranks.

#### What I would improve with no budget, time, or compute restrictions

- **Validate across multiple years and phases**, so the deviation becomes a distribution
  with a stated spread rather than a single figure.
- **Model the choice behaviour of candidates, not just the constraints.** The current
  simulator is constraint-driven; real cutoffs are shaped by what candidates actually
  choose, which is the largest unmodelled term.
- **Publish a per-prediction error breakdown** — where the model is accurate and where it
  diverges — instead of one aggregate rank distance.
- **Get the rule encoding reviewed by someone who administers the process**, so the policy
  reading is independently confirmed rather than self-asserted.
- **Backtest against a phase that had an unusual policy change**, which is the case most
  likely to expose a wrong rule interpretation.

#### Alternatives not chosen, and why

- **A machine-learning predictor trained on historical cutoffs.** Rejected: with the
  available history it would overfit and, worse, it would be uninterpretable. A
  constraint-based simulator can be inspected when it is wrong; a fitted model cannot.
- **Reporting a percentage accuracy instead of a rank distance.** Rejected because
  "accuracy" invites a definition I would get to choose. Rank distance from a published
  cutoff is a fact, and it does not let me pick a flattering denominator.
- **Shipping it as a product or seeking institutional endorsement.** Rejected. It is an
  independent project; claiming operational use would be exactly the kind of inflation
  that makes the rest of this resume untrustworthy.
- **Treating the 73-rank result as a headline achievement.** Rejected. It is a
  plausibility check that passed. The interesting engineering is the compression and the
  indexed search; the validation is what keeps me honest about them.

---

## Cross-project answers

Interviewers often ask the connecting question rather than a project question. These are
the short versions I keep ready.

- **"Which of these is your strongest work?"** AgentSwarm, and not because of the physics.
  Because it is the one where I built the thing that decides whether to believe the
  output, calibrated it against deliberate deception, and then published the defects it
  found. The 22 of 25 matters only because the same audit also reported 5 defects and
  located every one of them in prose.
- **"What is the common thread?"** Every one of these projects is mostly verification
  code. In all of them the interesting engineering was never getting the model to produce
  output — it was building the component that decides whether to believe the output.
- **"What is your biggest weakness in this work?"** Small n, and I have stopped pretending
  otherwise. Two of four agents self-assessed. The Phase 3 shocks tested the wrong swarm
  for their hypothesis. The Phase 4 liturgy was instructed, not emergent. One run for
  Awakening, one phase for mSeat, no external replication for BrandXY. The results are
  real and the sample sizes are small, and both of those are true at once.
- **"Are the papers yours?"** No. The authors are the swarm agents
  `A001_DarkMatter` / `A002_QuantumCosmos`. I built the system that wrote them. Paper 1 is
  a Zenodo preprint and is not peer-reviewed; Paper 2 was not submitted.
- **"Tell me about a result that argues against your own project."** Paper 2's
  self-audit. It found that the DESI (w0,wa) agreement is circular — the model's outputs
  are the DESI input constants — and that the S8 result is tuned, and it recommended
  against submitting the paper as a resolution claim. That is the pipeline catching its
  own overclaim, and it is the single best evidence I have that the audit layer does real
  work rather than producing favourable verdicts.
