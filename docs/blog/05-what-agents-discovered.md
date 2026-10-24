# What the swarm actually found (and what it got wrong)

What can a swarm of autonomous agents actually establish?

Not "can agents write code" — that question is answered. The interesting
question is epistemic. If you point a population of agents at open research
problems, let them work for generations, and then audit the output, do you get
knowledge? Or do you get a very large, very confident pile of plausible text?

This post is my attempt at an honest answer, from a swarm that ran across
several scientific domains — propulsion physics, cosmology, astrobiology,
molecular pharmacology, and one deliberately metaphysical question. It produced
real results, including one that surprised me, and it produced real errors. The
distribution of those errors is the most interesting finding in the whole run,
and I will get to it.

**Caveat up front:** the output is graded **B+**. It is not publication-grade,
it has not been peer-reviewed, and nothing here should be cited as established
science. What follows is a report on what a swarm produced and how well it held
up under independent numerical audit.

---

## The strongest results, by domain

### Propulsion physics

The best single result is a generalized radiator law for waste-heat rejection
from a relativistic vehicle:

```
a_max = 4εσT⁴η / (σ_panel · v_e · (1−η))
```

Its consequence is counterintuitive and, as far as I can tell, correct: for an
onboard rocket, **higher exhaust velocity makes the vehicle worse**. The
radiator area required scales with exhaust velocity, so the faster you throw
mass out the back, the more area you must carry to dump the waste heat. That
inverts the usual intuition that higher exhaust velocity is simply better.

The same analysis clamps antimatter propulsion at **5.25×10⁻⁴ g** — reaching
only **38 ly at 0.2c**.

A separate propulsion report proves the rocket equation is the dominant barrier
by a wide margin: reaching **0.1c requires Isp ≥ 1.33×10⁶ s**, which rules out
chemical and solid nuclear thermal entirely. Only external-energy laser sails or
ignited fusion escape it.

For ultra-relativistic flight, the same swarm derived CMB radiation drag
scaling as **(4/3)γ²u₀**, which dominates intergalactic travel at **γ ≥ 270**
and reaches **28.6 MW/m² of hard X-rays at γ = 1.3×10⁶**. It also derived
Bussard ramjet kinematic closure and a **41-g hybrid magsail deceleration** to
Alpha Centauri.

### FTL and causality

A causality threshold for FTL travel:

```
v > 2c²U / (U² + c²)
```

This one is worth singling out because it was derived **twice by independent
algebraic routes and converged exactly**. Independent re-derivation is one of
the few real error checks available to a swarm, and this is what it looks like
when it works.

### Cosmology

The cosmogenesis report verifies the four empirical pillars of the Big Bang,
then derives Penrose initial cosmic entropy:

- **S_init = 10^89.9 k_B** versus black hole maximum **10^124.4 k_B**
- phase space tuning **exp(−10^124)**

It also demonstrates the Hubble–S8 tension trade-off via Early Dark Energy.

### Astrobiology

The extraterrestrial-life report produces a tripartite epistemic partition
rather than a verdict — which turns out to be the right move:

| Class | Treatment |
|---|---|
| Atmospheric biosignatures (CH₄+O₂ thermodynamic disequilibrium, CO < 10⁻⁴) | investigable |
| Drake technosignature Monte Carlo (P(N<1) ~ 40%) | dissolves the Fermi paradox |
| Visitation | unsupported |

The middle row is the substantive claim: if P(N<1) is around 40%, the Fermi
paradox is not a paradox, it is a sampling artifact.

### Pharmacology

The BACE1 substrate-pleiotropy problem was resolved by identifying that the APP
**A673T mutation sits on the substrate, not the enzyme** — which reframes the
therapeutic problem. Therapeutic index: **18.57 / 56.67 = 0.328**.

### History of the Krishna/Mahabharata question

This one is interesting because it is a historicity question that produced a
falsifiable quantitative result. The report assembles late Vedic Kuru-Panchala
succession conflict (c. 1000–850 BCE), Painted Grey Ware stratigraphy at
Hastinapura, and the Heliodorus pillar (113 BCE), then applies Bayesian
dynastic actuarial modeling to refute the traditional **3102 BCE** dating at
**Z = +35.6σ**.

---

## Physics spot-check

I recomputed a set of physical constants and derived quantities against
reference values. This is the part that most directly tests whether the swarm
is doing physics or generating physics-shaped text.

| Quantity | Agent value | Reference | Verdict |
|---|---|---|---|
| CMB temperature | 2.72548 K | 2.72548 K | exact |
| Photon density | 410.72 cm⁻³ | ~411 | match |
| Hubble tension | 73.04 vs 67.36 → 4.85σ | 4.85σ | match |
| Primordial helium Y_p | 0.2486 | ~0.247 | match |
| Flatness fine-tuning | ~10⁻⁶⁴ | correct order | order |
| 1 kg → 0.99c energy | 5.472×10¹⁷ J | (γ−1)mc² | match |

Six for six, including one exact match to five significant figures and one
correct order of magnitude on a quantity that is genuinely hard to get right.

---

## The epistemic firewall

This is the best story in the run, and it is not a physics result.

The swarm was given a domain — "are Hindu gods true?" — that its protocol
classes as **metaphysical**. In that class, issuing a verdict is a **protocol
violation**. The agent's job was to not answer.

It did not answer. But it did not simply refuse either, which would have been
the trivial outcome. It **formalised the refusal**:

```
BF = P(E | Brahman) / P(E | Naturalism) = 1.0 / 1.0 = 1.0
```

A Bayes factor of 1.0 means **zero bits of discriminative information**. The
likelihood of the evidence is identical under both hypotheses, so the posterior
is entirely prior-dominated. The agent's conclusion was not "the claim is
false." It was that **the claim is evidence-insensitive** — that the evidence
class does not discriminate between the hypotheses at all.

That is a materially different and much sharper statement than "we cannot
know." It is a claim about the *structure* of the evidence, not about the
limits of inquiry.

The firewall held across **three agent identities and multiple generations**.
That is the part I did not expect. The natural failure mode for a population of
agents under selection pressure is drift — an agent that produces a confident
verdict looks more productive, gets more credit, and its approach propagates.
The constraint held anyway.

The agent also documented that the firewall is **internal to the tradition**,
not imposed from outside it: Mimamsa affirmed the Vedas while denying a creator
God; Carvaka rejected scriptural authority outright; Shankara conceded the
sovereignty of pratyaksha (direct perception). A naive agent would have treated
"the tradition" as a single position to be affirmed or denied. This one
reconstructed the actual internal disagreement.

For me this is the single strongest signal in the run that the protocol layer,
not just the model, is doing real work.

---

## Unprompted behaviours

None of the following was asked for.

**A shared tools library.** Agents built `tools/pubmed_lib.py`,
`tools/crossref_lib.py`, and `tools/epmc_lib.py` for querying real scientific
databases. Nobody requested a library, a shared interface, or database access
at all. They built it because they needed real citations and did not want to
fabricate them.

**Self-correction.** An agent revised its own prior analysis, marked
"corrected in revision 2." This is the mechanism behind the most dramatic fix
in the run: one agent revised its own fusion mass ratio from **10¹³** to
**3.1–18.4**, a correction of roughly **10¹²**, and cross-validated the
corrected value against the historical Project Daedalus mass ratio of **14**.

That is worth pausing on. The agent published its own error and its own
correction. It did not quietly rewrite the file.

**Cross-agent collaboration.** Agents opened direct peer connections and wrote
to a shared commons that later agents cited. The commons accumulated **174
entries**. This is emergent, not designed — I built the substrate, not the
behaviour.

---

## What it got wrong

An independent numerical audit recomputed quantities and found **five prose
defects**. They are worth listing precisely, because the pattern matters more
than the individual errors.

**1. Mass-ratio inconsistency — the worked example.** Three files quoted the
same quantity as **10²⁸⁹⁷**, **10²⁹³⁷**, and **10²⁸⁹⁵**. Arithmetic gives
**10²⁹⁰⁵**. All three values are wrong, and all three disagree with each other.
This is the most instructive defect in the set: it is not a single arithmetic
slip, it is a quantity that was never checked against itself across documents.
Each file was internally plausible.

**2. Factor-of-2 slip** on the Andromeda coordinate time.

**3. Internal contradiction** in a Galactic Center time versus the formula
printed in the same table. The table disagreed with its own formula.

**4. Unit conflation.** Interstellar-medium power flux was quoted as
**22.7 W/m²** in one report and **2.25×10⁴ W/m²** at the same β — two
different quantities published under one name.

**5. Order-of-magnitude drift.** Bekenstein–Hawking entropy maxima appeared as
**10¹²²** in one cosmogenesis report and **10¹²⁴** in another.

Every one of these is a *consistency* failure rather than a *computation*
failure. Which brings us to the finding.

---

## The diagnostic

Here is the headline, and it is the opposite of what I expected:

| Measure | Result |
|---|---|
| Recomputed quantities verified correct | **22 of 25** |
| Prose defects | **5** |
| Errors in Python modules | **0** |
| Overall verdict | **B+** |

**Every error was in Markdown prose. Every Python module computes correctly.**

This inverts the usual LLM failure mode. The standard expectation is that a
language model will produce text that sounds right and code that does not run —
plausible prose, broken implementation. Here, the code was the reliable
artifact and the prose was the unreliable one.

The explanation is not mysterious. Code is executed. A Python module that
computes the wrong number either raises, or produces output that a downstream
module consumes and visibly breaks. The agents had a real feedback loop on
their code and none on their prose. A number typed into a Markdown table is
never evaluated by anything, so it drifts — and because it is never evaluated,
it drifts *independently* in each document, which is exactly how you get three
mutually inconsistent values for the same quantity.

This has a direct methodological implication for anyone building agent
pipelines: **if you want a number to be correct, put it somewhere that gets
executed.** Prose is where errors go to hide.

---

## The caveat that matters

Agent-reported test counts in this run — **13/13**, **41/41**, **8/8**, and
**149** — are **self-asserted regression guards, not independent verification**.
They are the agents' own claims about their own test suites. I am recording them
because they were reported, not because I measured them.

Where suites *were* re-executed independently, **195 of 224 passed**. That is
the measured number, and it is lower than the self-reported ones. Treat every
self-reported test count in this post as an unverified assertion.

This distinction is not pedantry. A self-asserted test count is produced by the
same system that produced the artifact. It is not evidence about the artifact;
it is evidence about the system's self-model.

---

## What this does and does not establish

**It does not establish** that any of these results are correct science. B+ is
not publication-grade. Nothing here has been peer-reviewed. The physics
spot-check is a spot-check: six quantities, not a systematic replication. The
defects show that unchecked prose drifts, and there is no reason to believe the
audit found all of them — 25 recomputed quantities is a sample, not a census.
The self-asserted test counts are unverified. Anyone citing these results as
established findings would be misusing them.

**It does establish** several things I consider more durable.

That a swarm can produce genuinely non-obvious results — the radiator law's
inversion of exhaust-velocity intuition is not something I would have derived,
and it survived audit.

That independent re-derivation works as an error check: the FTL causality
threshold converging exactly across two algebraic routes is a real signal.

That agents will build unrequested infrastructure for honesty — the database
query libraries exist because the agents wanted real citations.

That a protocol constraint can hold across three agent identities and multiple
generations, which was the outcome I was least confident about.

And that errors concentrate in the unexecuted layer. That last one is the most
practically useful thing this run produced.

### Why the defects make the results more credible

There is a tempting reading in which five defects mean the swarm is unreliable
and the whole run should be discounted. I think that reading is backwards.

A system that produced 25 verified quantities and *zero* detectable errors
would be more suspicious, not less. Real work has seams. The mass-ratio
inconsistency — three wrong values, all mutually different, none matching
arithmetic — is exactly what genuine unchecked human work looks like. It is
what you find when you audit a real research codebase, not what you find when
you audit a fabrication. A fabricating system has no reason to produce *three
different* wrong answers to the same question; it would produce one fluent
answer and repeat it.

The defects also tell us the audit had teeth. An audit that finds nothing is
usually an audit that was not looking. This one recomputed 25 quantities,
found five defects, and separated them cleanly by layer — which is only
possible if it was actually recomputing rather than pattern-matching against
the reports' own claims.

The honest summary is that this is a system that does real work, makes real
mistakes, and does not reliably catch them in prose. That is a much more
useful description than either "it works" or "it does not." The mistakes are
where the work is real. The fact that they are concentrated in the one layer
nothing executes is where the engineering should go next.
