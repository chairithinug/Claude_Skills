---
name: token-optimizing
description: >
  Compresses prompts, system instructions, RAG context, few-shot blocks,
  agent loops, or any LLM input/output for lower token cost and latency
  without losing load-bearing information. Use whenever the user shares
  a prompt and asks to "shorten," "optimize," "compress," "trim," "tighten,"
  "reduce tokens," or "cut costs"; whenever the user complains about LLM
  bills, latency, context-window pressure, or rate limits; whenever the
  user pastes a system prompt, few-shot block, RAG pipeline, or agent
  scaffold for review; whenever the user types /token-optimizing; or
  whenever a prompt the user is iterating on is visibly bloated. Applies
  a prioritized triage (measure → cache → batch → route → bound → compress
  → rewrite) rather than blind shortening, and produces a measurable
  before/after with a load-bearing verification checklist.
---

# /token-optimizing — Token Optimization Skill

Compress LLM workloads for cost, latency, and energy **without losing
load-bearing information**. The unit of success is *quality per token*,
not minimum tokens. A 30% cut that breaks one edge case is a worse
trade than a 10% cut that's safe.

## When to use this

- User explicitly invokes `/token-optimizing`.
- User asks to shorten / compress / tighten / reduce tokens / cut costs
  on a prompt, system message, RAG context, few-shot block, or agent.
- User complains about bills, latency, or context limits.
- User pastes a long prompt and asks for review or feedback.
- The shared prompt shows obvious bloat (>1.5k tokens of system instructions,
  repeated reminders, ten near-identical few-shots, dumped full documents).

## Core principle

**Preserve load-bearing content. Compress everything else.** If the case
for a chunk staying cannot be defended, it goes. If the case for a chunk
going cannot be defended, it stays.

---

## Step 0 — Triage before touching the prompt

Most teams over-index on rewriting the prompt because it's the visible
artifact. The bigger wins are usually upstream. Run this triage first
and tell the user which lever applies *before* compressing text.

| Lever | Typical savings | When it applies |
|---|---|---|
| **Prompt caching** | 50–90% on repeated input | Same system prompt / docs / tools called >2× |
| **Batch API** | ~50% flat | Workload tolerates async (evals, bulk processing) |
| **Model routing / cascade** | 40–80% | Mixed difficulty — most queries are easy |
| **RAG instead of stuffing** | 60–95% | Large corpus, only fragments needed per call |
| **Output bounding** | 20–50% | No `max_tokens`, no length spec, verbose CoT |
| **Prompt rewriting** | 10–30% | After the above; usually the smallest lever |

**Rule:** if the user has not turned on prompt caching and is repeating
the same context, fix that first. Rewriting a prompt that's about to be
cached is rearranging deck chairs.

---

## Step 1 — Identify load-bearing content

Before cutting anything, mark each block in the input as **KEEP**,
**COMPRESS**, or **CUT**.

### KEEP (load-bearing — never cut, never paraphrase loosely)

- The task definition / objective (one clear sentence minimum).
- Output format and schema constraints (JSON shape, length, language).
- Hard constraints ("must include X", "must not mention Y").
- Domain terminology that changes the output if dropped.
- Few-shot examples that demonstrate **distinct** edge cases.
- Safety / legal / medical / financial caveats when the domain warrants.
- Citations, provenance, source attribution.
- Variables and slots that change per call.
- Calibration anchors (numbers, dates, units, named entities).

### COMPRESS (rewrite shorter, keep the meaning)

- Verbose role descriptions ("You are a brilliant, world-class expert
  with 30 years of experience…" → "You are a [role].").
- Multi-paragraph rationale that can become a sentence.
- Long enumerations that can become structured lists.
- Repeated terms that can be aliased once.
- Verbose schemas that can become compact JSON / TypeScript types.
- Few-shot examples that are *near-duplicates* of each other.

### CUT (no semantic load — remove entirely)

- Politeness padding ("please," "kindly," "if you could," "thank you").
- Self-praise framing ("you are amazing", "you always do great work").
- Repeated safety/role reminders sprinkled across the prompt.
- "Take a deep breath / think step by step" if the model already does CoT.
- Filler transitions ("Now, with all that in mind, let's begin.").
- Comments inside the prompt explaining the prompt to a human reader.
- Any instruction that contradicts another instruction (resolve, then cut).

---

## Step 2 — Apply compression techniques in priority order

Within the prompt itself, apply these in order. Stop when token budget
or quality target is met — don't over-compress.

### 2a. Structural

1. Move stable content (system prompt, tool defs, docs) to the **front**
   so it caches. This alone often eliminates 50–90% of recurring cost.
2. Replace prose constraints with **structured tags** (XML, JSON,
   bullets). Structure is denser than narration.
3. Collapse **redundant sections** — if "rules" and "guidelines" overlap,
   merge them.

### 2b. Few-shot

4. Test with **0 → 1 → 3 → 5** examples on a held-out set. Most tasks
   plateau at 2–3 well-chosen examples. More is decoration.
5. Choose examples that are **maximally different** from each other and
   each demonstrate a distinct edge case. Drop near-duplicates.
6. Compress example **inputs** (the part the model is conditioning on
   the *shape* of), not the outputs (which it's learning to emit).

### 2c. Lexical

7. Imperative > polite. "Do X." beats "Please could you help me to do X."
8. Define long terms once, alias short. ("the document, hereafter D.")
9. Cut hedges and intensifiers ("very," "really," "extremely," "kindly").

### 2d. Output side

10. Set `max_tokens` honestly. Caps protect against runaway generations.
11. Specify length: "Answer in ≤3 sentences" or "≤150 words."
12. Use **stop sequences** for known terminators.
13. Skip CoT when the task is trivial (extraction, classification).
14. Don't ask for rationale that will be discarded.
15. Use **structured output** (JSON / tool calls) when downstream
    parsing — but only if the schema cost < parsing benefit.

### 2e. Context

16. RAG, don't stuff. Retrieve top-k, rerank, send the smallest set
    that contains the answer.
17. Summarize stable history once, reuse the summary.
18. Prune conversation: keep system + last N turns + rolling summary.
19. Gate tool definitions per step. Tool schemas are tokens too.

---

## Step 3 — Watch for tokenizer surprises

Token counts are not character counts and not the same across models.

- **Thai, Japanese, Chinese, Arabic** typically tokenize 2–4× worse than
  English on most BPE tokenizers. A "short" Thai prompt is often longer
  in tokens than its English equivalent.
- **Code, JSON, URLs, UUIDs** tokenize poorly — lots of single-character
  or unusual-byte tokens. Compressing JSON keys (`"customer_first_name"`
  → `"fn"`) can save real tokens.
- **Whitespace and indentation** are tokens. Trim trailing spaces, avoid
  unnecessary blank lines, but don't sacrifice readability of constraints
  the model has to follow.
- **Always count tokens with the actual tokenizer** of the target model
  (`tiktoken`, Anthropic's tokenizer endpoint, etc.) — character heuristics
  lie, especially for non-English content.

If the user's workload is Thai/CJK/code-heavy, flag this — they may be
paying 3× the tokens they expect.

---

## Step 4 — Verify nothing load-bearing was lost

Before delivering the optimized version, run this checklist against the
original. Every "yes" is required.

- [ ] Task definition still present and unambiguous?
- [ ] All hard constraints preserved?
- [ ] Output format / schema preserved?
- [ ] All distinct edge cases still represented in examples?
- [ ] Safety / domain caveats preserved where the domain demands them?
- [ ] Citations / provenance / source attribution intact?
- [ ] Per-call variables and slots untouched?
- [ ] Behavior on a sample input is plausibly the same?

If any answer is "no" or "unsure," restore the cut content. Do not
ship a compression that cannot be defended.

---

## Output format

Deliver the result in **this exact structure**:

### 1. Diagnosis (3–6 bullets)
What was bloated, what was load-bearing, what bigger lever applies (if any).
If a non-rewrite lever (caching, batching, routing, RAG) would dominate
this rewrite, **say so first** — don't bury it.

### 2. Optimized version
The actual compressed prompt, in a code block, ready to paste.

### 3. Diff explanation (compact table or bullets)
What was kept, what was rewritten, what was cut, with a one-line reason
each. Group by category, not line-by-line.

### 4. Token estimate
Rough before/after counts (state which tokenizer is being approximated —
e.g., "cl100k / Claude tokenizer, ±10%"). For non-English, count with
the real tokenizer or flag the uncertainty.

### 5. Verification checklist
The Step 4 checklist, filled in.

### 6. Bigger levers (if any)
One paragraph: caching, batching, routing, RAG, model choice, eval setup.
Numbered if there's more than one.

No sycophantic opener, no trailing summary.

---

## Edge cases

**The prompt is already tight.** Say so. Don't manufacture compressions
to look productive. Suggest non-rewrite levers instead.

**The user wants aggressive compression and the prompt is safety-relevant.**
Refuse aggressive cuts on safety content. Offer compression on the
non-safety scaffolding only, and explain why.

**The user shares only a fragment.** Ask once for the full prompt and
the call frequency (helps decide if caching is the bigger lever). If
they decline, optimize what's visible and flag the limitation.

**The prompt is a few-shot block with 8+ examples.** Compress aggressively
on this — few-shot is usually the largest cuttable surface. But verify
edge-case coverage before cutting.

**The user is on Thai/CJK/code-heavy workloads.** Run the tokenizer note
(Step 3) prominently. The biggest "savings" may be using the right
tokenizer math, not rewriting the prompt.

**The user mentions a specific provider (Anthropic, OpenAI, Google).**
Caching pricing and batch discounts differ. Don't quote numbers from
memory — direct them to current pricing pages and frame savings as
"X% of input cost" patterns.

---

## Reference files

- [`references/worked-example-customer-support.md`](references/worked-example-customer-support.md)
  — Full worked example on a realistic agent system prompt (~2,900 → ~950
  tokens, 67% reduction). Read this when the user shares a multi-section
  agent prompt with tools, examples, and rules — the patterns generalize.
  The inline mini-example below is a primer; the reference file is the
  deep dive.
- [`evals/trigger-eval.json`](evals/trigger-eval.json) — 20 trigger test
  cases (13 positive + 7 negative) for use with skill-creator's
  `run_loop.py` to optimize this skill's description.
- [`evals/quality-eval.md`](evals/quality-eval.md) — 8 graded bloated
  prompts of varying severity (mild bloat → safety-relevant →
  already-tight → Thai tokenizer stress test) for benchmarking output
  quality.

---

## Worked example (compressed)

**Before** (≈180 tokens):

```
You are an extremely talented and helpful AI assistant with deep expertise
in customer support. You always do an amazing job. Please carefully read
the following customer message and, taking a deep breath and thinking step
by step, kindly classify it into one of these categories: billing, technical,
account, or other. Please make sure to be accurate. Please return your
answer. Thank you so much for your help!

Customer message: {message}
```

**After** (≈35 tokens):

```
Classify the customer message into one of: billing, technical, account, other.
Return only the label.

Message: {message}
```

**Diff**: cut role flattery, cut "take a deep breath" (CoT not needed for
single-label classification), cut politeness padding, made the output
contract explicit ("return only the label"). Kept: task, label set,
variable slot. Estimated savings: ~80% on this prompt; if called 10k
times/day, prompt-caching the system portion is still the bigger win.

---

## One-line rule of thumb

**Cache first, batch second, route third, bound fourth, compress fifth,
rewrite last. The cheapest token is the one not sent.**
## Anti-patterns to flag and refuse

- **Compressing without an eval set.** Refuse to ship aggressive cuts
  on safety- or revenue-critical prompts without a verification path.
  Suggest the user build a 50-example eval first.
- **Compressing safety-relevant content** in medical, legal, mental-health,
  financial, or crisis-adjacent prompts. The few tokens saved are not
  worth the liability.
- **Removing citations** to save tokens. Provenance is load-bearing in
  any prompt that touches research, journalism, or compliance.
- **PII inside cached prompts.** Caches are storage; storage has
  compliance implications.
- **Single-pass compression on long agent prompts.** Agent prompts often
  need *multiple* small compressions (system + tools + history + each
  turn) — compress the right layer, not the easy layer.

---

