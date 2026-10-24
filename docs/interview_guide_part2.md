# Interview Guide — Part 2

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
