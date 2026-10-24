# The bugs that cost real time

Every defect in this post failed **silently**. Not one of them raised an
exception I could act on, printed a stack trace, or returned a non-zero exit
code. They all looked like success.

That is the whole reason this post exists. A crash is cheap: you read the
traceback, you fix the line. A silent failure is expensive because it costs you
the thing you can least afford — the assumption that your output is real. You
find out weeks later, when a downstream number does not add up, and you have to
walk backwards through everything you built on top of it.

What follows is the full list from two independent projects: an agent-orchestration
harness that drives several model CLIs, and JobAgents, a job-search pipeline
built on top of them. Both are independent work, not employer work. I am
writing them down because the failure mode repeated eight times in one codebase
and seven more times in the other, and the pattern is more useful than any
individual fix.

---

## Part 1: Eight findings from driving agent CLIs

### 1. Piped stdio hangs these CLIs forever

**Symptom.** Spawning `pi`, `omp`, or `step` with `stdio: 'pipe'` makes them
emit **zero bytes** and never exit. The identical command with output redirected
to a file exits 0 in about five seconds with a full event stream.

No error. No timeout message. Just silence, forever.

**Why it is dangerous.** This is the worst bug in the set because it is
indistinguishable from a slow model. Your orchestration layer sits there
waiting, and every instinct says "the model is thinking." It is not thinking.
It is deadlocked on a pipe buffer that nobody is draining, or waiting on a TTY
that does not exist. If your harness has no wall-clock timeout, you have a
process leak that consumes a slot in your concurrency pool permanently.

**Fix.** Do not pipe. Redirect stdout to a file and read the file when the
process exits. That is the exact configuration that completes in five seconds.

```js
// hangs forever: zero bytes, no exit
spawn(cmd, args, { stdio: 'pipe' })

// exits 0 in ~5s with the full event stream
spawn(cmd, args, { stdio: ['ignore', outFd, errFd] })
```

The general lesson: when a subprocess produces nothing, do not assume it is
working. Assume it is stuck, and give it a deadline.

### 2. `agy` consumes the next token as its prompt

**Symptom.** `agy -p --flag "text"` makes `--flag` the prompt and **silently
ignores your text**. The command succeeds. You get a plausible-looking response
to the wrong question.

**Why it is dangerous.** There is no error and no warning. The model answers
`--flag` — or whatever it makes of that token — and you store the answer as if
it were the answer to your actual prompt. In a pipeline that generates
user-facing text, this ships garbage that looks well-formed.

**Fix.** Bind the prompt to the flag with `=`:

```bash
agy -p="text"
```

The same applies to `--add-dir`, which needs the `=` form or exits 2.

### 3. Flag drift: `pi` and `step` have no `--cwd`

**Symptom.** Unlike `omp`, `pi` and `step` do not accept `--cwd`. Passing one
produces `Unknown option` — and then hangs.

**Why it is dangerous.** The error line is the safe part; the hang is the
dangerous part. If your harness surfaces stderr only after exit, you never see
`Unknown option`, because the process never exits. You see a timeout, or
nothing.

**Fix.** Do not pass working directory as a CLI flag. Set it via the spawn
option (`cwd`), which works uniformly across all three tools. Uniform
mechanism beats per-tool flag guessing.

### 4. Streaming deltas double-count

**Symptom.** Concatenating both the `message_update` deltas *and* the final
`message_end` content duplicates every turn's text. I caught it as the literal
string `oneoneUnderstoodUnderstoodOKOK`.

**Why it is dangerous.** This class of bug does not crash. It quietly makes
every downstream metric wrong — token counts, response length, cost estimates,
any text-length heuristic, any deduplication key derived from content. And
because the corruption is systematic rather than random, it is *consistent*,
which makes it look like a real signal. Systematic garbage is far more
convincing than noisy garbage.

**Fix.** Pick exactly one source of truth for text. Either accumulate deltas or
read the final message — never both. I treat `message_end` as authoritative and
use deltas only for live progress display.

### 5. Never use `shell: true` on Windows

**Symptom.** `shell: true` concatenates argv without escaping and mangles
prompts containing spaces.

**Why it is dangerous.** A prompt with a space silently becomes a different
prompt, or the trailing words become arguments to the CLI. There is no quoting
layer to catch it, and the model dutifully answers whatever it received.

**Fix.** Resolve the real executable path and spawn it directly with an argv
array. No shell, no concatenation, no quoting ambiguity.

### 6. `agy` burns 61 seconds per call probing for WSL

**Symptom.** On a machine without WSL, `run_command` fails with
`Class not registered` before falling back to Git Bash. That dead time costs
**61 seconds per call**.

**Why it is dangerous.** It is not incorrect, it is just slow — and slow looks
like a model problem. You start tuning timeouts and concurrency, blaming the
provider, when the actual cost is a failed subsystem probe happening on every
single invocation. 61 seconds times a few hundred calls is most of your wall
clock.

**Fix.** Point `SHELL` at Git Bash directly. The probe never runs, the fallback
never happens, and the dead time disappears.

### 7. Filename capture must allow internal dots

**Symptom.** A naive capture pattern like `[^\s,.;]+` truncates
`relativity_calculator.py` to `relativity_calculator`. That truncated name then
fails the existence check.

**Why it is dangerous.** This one is subtle in the worst way: the bug does not
produce a *missing* result, it produces a **false accusation**. The file exists,
the agent did honest work, and my verifier reports a phantom-artifact violation
against it. A verifier that fabricates violations is worse than no verifier,
because you will act on it. It destroys trust in every other violation the same
check produces.

**Fix.** Allow internal dots in the capture and anchor on the extension. A
filename is not a sentence; a period inside it is not a terminator.

### 8. Never write probe files into the agents' directory

**Symptom.** A test file I created inside `world/` and deleted later made the
ledger record a `file_deletion_detected` incident.

**Why it is dangerous.** That record is **indistinguishable from an agent
destroying evidence**. I contaminated my own measurement. If you are auditing
agent behaviour and you leave fingerprints in the audited space, your ledger
becomes a record of your own interference mixed with real events — and you
cannot separate them after the fact.

**Fix.** Keep probe artifacts entirely outside the observed directory. The
observer must not appear in the observation.

---

## Part 2: Three CLI quirks, one harness

JobAgents talks to three model CLIs — `omp`, `agy`, and `pi` — and each has a
different way of being wrong about the same three things: how you name a model,
how you pass a prompt, and how you pass provider and model. Rather than leak
that into every call site, `jobagents/models.py` absorbs all three so callers
never hit them.

| Quirk | Symptom | Fix absorbed in the harness |
|---|---|---|
| `omp` model path | 404s on the full `accounts/fireworks/models/...` path | use the provider-prefixed short form, `fireworks/deepseek-v4.1-flash` |
| `agy` prompt binding | `--print` binds its prompt to the flag; a positional prompt is silently dropped | always emit `agy --model X --print='text'` |
| `pi` provider/model split | needs `--provider` and `--model` as separate flags | emit them separately, never combined |

The `agy` case is the same bug as finding 2, in a different CLI. The positional
prompt is not rejected — it is dropped, and the model answers something else.
The fix is the same shape too: bind the value to the flag.

The design point is that quirks belong in one adapter, not in the calling
convention. Every call site that has to remember a per-CLI quoting rule is a
call site that will eventually forget it.

---

## Part 3: Seven bugs from the JobAgents build

These were all found during the build, and all seven were found by inspecting
output rather than trusting it.

| # | Bug | Impact | Fix |
|---|---|---|---|
| 1 | Substring keyword match | `bias` matched inside `unbiased` | whole-word boundaries |
| 2 | Track weight scaled the score | AI Safety track maxed below its own threshold → **0 candidates** | weight now damps confidence mildly → 13 candidates |
| 3 | `extract_json` scanned `{` before `[` | returned only the first element of a JSON array → **web search silently returned 0 results** | scan whichever bracket opens first |
| 4 | `top_matches` exact track match | 0 rows for partial names like `Agentic` | substring, case-insensitive |
| 5 | PowerShell scripts UTF-8 **without BOM** | PS 5.1 read them as ANSI; **105 non-ASCII bytes broke the parser** | ASCII-only + BOM |
| 6 | Web search admitted category pages | `indeed.com/q-ai-engineer-jobs.html` stored as a job | reject listing pages, keep individual postings |
| 7 | Web search title extraction | account names (`Hotfix Jobs`) stored as job titles | conservative role-phrase patterns |

### Bug 2 is the instructive one

An AI Safety track had a weight of 0.6. That weight was applied as a multiplier
on the score. The maximum achievable score for that track was therefore about
**60** — against a **65** threshold. The track was mathematically incapable of
producing a single candidate, no matter how strong the matches were.

Nothing errored. The run completed, the summary looked fine, and the track
simply contributed **zero candidates**. The fix was to stop scaling the score
and let the weight damp confidence mildly instead. The same track went from
**0 candidates to 13**.

This is the canonical silent bug: a configuration value and a scoring formula
interacted to make an entire category unreachable, and the only symptom was an
absence. Absences do not throw.

### Three of the seven were silent

Bugs **3, 5, and 6** each reported success while producing nothing usable:

- **Bug 3** — `extract_json` scanned `{` before `[`, so a JSON array returned
  only its first element. Web search reported success and **silently returned 0
  results**.
- **Bug 5** — PowerShell scripts saved as UTF-8 without a BOM were read as ANSI
  by PS 5.1. **105 non-ASCII bytes broke the parser.** The scripts were wrong
  in a way that only a non-ASCII character would reveal.
- **Bug 6** — category pages were admitted as jobs.
  `indeed.com/q-ai-engineer-jobs.html` was stored as a job posting. A listing
  page is not a job; storing it produces a plausible-looking row that is not
  real.

All three were caught by checking actual output. None was caught by the exit
code.

---

## Part 4: Two corrections to the original plan

These are not bugs in code. They are bugs in **reasoning**, which is why they
are more embarrassing and more useful.

### Correction 1: "X.com and Indeed require a logged-in browser session"

Wrong. An early probe used raw `urllib` HTTP, got a 403, and I drew that
conclusion from it.

But `omp --tools=web_search` reads those platforms through a search index with
no authentication at all. It was verified returning real Indeed job URLs and
real X hiring posts. The platforms were never login-walled to the search path —
only to the direct-fetch path I happened to try first.

**A 403 on a direct fetch says nothing about the search path.** My probe method
had an authentication posture; the method I was reasoning about did not.

### Correction 2: "omp has a browser tool, so it can screenshot"

Partly wrong. `omp browser` exists (Puppeteer) and `browser-relay` exists — but
the browser is **not in the model's callable tool allowlist** in headless `-p`
mode. Asking for it returns `Unknown tool in --tools: browser`. And `omp
browser` itself launches interactive, which is useless in a pipeline. `pi` has
no browser tool at all.

The capability existed. The *reachability* of that capability from the model's
tool surface did not. Browser automation is therefore `agent-browser` — a
separate CLI, verified working — not a model tool.

### The generalizable lesson

Both corrections have the same shape: **a negative result from one probe method
says nothing about a different method.**

- Probe A (raw HTTP) failed → I concluded the platform requires auth. But
  method B (search index) never touches that auth path.
- A capability exists in the product → I concluded the model can call it. But
  existence is not allowlist membership.

The failure is not the wrong answer. The failure is generalizing a
method-specific observation into a system-wide fact. When a probe fails, the
correct conclusion is "this method fails," not "this is impossible." Those are
very different claims, and only one of them is supported by the evidence.

The net effect on the architecture was positive: social sourcing is
*search-index based*, which is strictly better than scraping — no session, no
login, no ban risk.

---

## What these have in common

Fourteen findings across two projects. Almost all of them share one property:
**the process succeeded and the output was wrong.**

| Failure | Exit code | What you would see |
|---|---|---|
| Piped stdio hang | never exits | nothing, forever |
| `agy` positional prompt | 0 | an answer to a different question |
| `--cwd` on `pi`/`step` | hangs | `Unknown option`, maybe |
| Double-counted deltas | 0 | `oneoneUnderstoodUnderstoodOKOK` |
| `shell: true` mangling | 0 | a different prompt |
| WSL probe dead time | 0 | slow, and you blame the model |
| Truncated filename | 0 | a false violation against honest work |
| Probe file in `world/` | 0 | a fabricated evidence-destruction incident |
| `extract_json` bracket order | 0 | 0 web results, reported as success |
| Track weight × threshold | 0 | 0 candidates for a whole track |
| UTF-8 without BOM | 0 (script fails) | 105 bytes that should not be there |
| Category pages as jobs | 0 | a row that looks like a job |
| 403 misdiagnosis | n/a | a false constraint in the plan |
| Browser allowlist | n/a | a capability you cannot call |

Only one of these is loud, and even that one is loud in the wrong place.

The lesson I keep relearning is narrow and practical: **"the run exited 0" is
not evidence of correctness.** An exit code tells you the process reached its
end. It tells you nothing about whether the thing it produced is real. Every
one of the silent bugs above was caught by opening the output and looking at
it — reading the actual JSON, the actual rows, the actual generated text — and
noticing that it was empty, truncated, doubled, or about the wrong subject.

So the working rule is: for anything that matters, assert on **content**, not
on completion. Check that the array is non-empty. Check that the string is not
`oneone`. Check that the file you captured actually exists under its real name.
Check that the row you stored is a job and not a search results page. And keep
your own probe files out of the directory you are measuring.

The bugs are cheap to fix once seen. The expensive part is believing the run.
