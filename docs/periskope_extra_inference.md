# Periskope — extra question

## Describe your experience with inference, KV cache, tokenomics

I'll separate what I've measured from what I haven't, because you'd find the gap in
five minutes and it's more useful to you if I mark it myself.

**Tokenomics is the part I've actually done.** My job pipeline computes **22,839
match scores with zero model calls** — a deterministic scoring stage acts as a
cost gate, and only candidates above a threshold ever reach an LLM. Driving the
cost of the filter stage to zero is the single highest-leverage inference decision
I've made. I also run hard budget caps per agent run and audit tool calls
per-turn (**15,317 tool calls across 84 turns** in one security-research
workload), so spend is bounded by construction rather than by watching a
dashboard.

**I've measured inference cost across substrates.** I ran a controlled benchmark
of four agent harnesses on an identical task, capturing **cost per turn, tools per
turn, thinking tokens per turn, and fresh-token volume**. Two harnesses on the
*same underlying model class* differed by more than an order of magnitude in cost
per turn, and one carried zero marginal cost while moving ~22× more fresh-token
volume. That result is why I treat "which model" as a much weaker question than
"which harness, with what context, at what cost per successful turn."

**I've been bitten by token accounting.** A streaming integration I wrote summed
both the incremental deltas *and* the final message payload, double-counting every
turn's text — I caught it only after seeing `oneoneUnderstoodUnderstoodOKOK` in
output. It never crashed; it silently corrupted every downstream metric. Token
counts that are wrong by construction are worse than no counts, because you make
routing and budget decisions on them.

**Context budgeting is a daily concern.** I bound a long-running agent's living
memory to **under 4,000 words**, and I keep the ground-truth block in generation
prompts deliberately compact — a bigger context is not free, it's a per-call tax.
I recently cut a pipeline's per-call latency roughly **5× (87.5s → 16.5s)** by
replacing a large coding-assistant system prompt with a lean one; less prefill per
call, and the model stopped behaving like an agent when I only wanted text.

**Where KV cache sits in my understanding.** Prefill is compute-bound and
processes the whole prompt; decode is memory-bandwidth-bound and grows the cache
by one token per step. The cache scales with context length × layers × KV heads ×
dtype, so on agent workloads the transcript — not the model weights — becomes the
binding memory constraint, and it's why long multi-turn transcripts get
disproportionately expensive while a repeated system prompt is the obvious thing
to reuse via prefix caching. I've also worked the memory-saving side of the same
coin: **QLoRA fine-tuning of a 20B model** (4-bit quantized base) on AMD MI300X
GPUs, where the whole game is fitting the work into the memory you have.

**My honest boundary:** I have not operated a serving stack — no vLLM, TGI or
TensorRT-LLM in production, no paged-attention tuning, no custom kernels. My
inference experience is client-side: measuring it, budgeting it, routing around
it, and being on the hook when a context got too big or a cost model was wrong.
Given that Periskope's agent answers customer conversations concurrently, the KV
cache is where your throughput and unit economics actually live, and that's a
layer I want to work in rather than claim I already own.
