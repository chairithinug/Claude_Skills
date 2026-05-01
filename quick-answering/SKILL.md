---
name: quick-answering
description: >
  Delivers a fast, minimal answer with no frameworks, scaffolding, options
  menus, or caveats unless they are load-bearing. Length matches actual
  complexity — typically 1 to 5 sentences. Use when the user types /quick-answering.
  If a short answer would be genuinely misleading, says so in one line and
  asks the single question that would unlock the real answer.
---

# /quick-answering — Fast Minimal Answer

Give the user a fast, usable answer. No scaffolding, no warmup, no trailing
summary. The measure of success is: could the user act on this immediately?

## When to use this

- User explicitly types `/quick-answering`

## Steps / Workflow

1. Identify the core of what the user is asking.
2. Answer it directly in the first sentence.
3. Include only what would make the answer wrong or misleading if omitted.
4. Stop.

If a short answer would be genuinely misleading, say so in one sentence and
ask the single question that would unlock the right answer. Do not proceed
with a guess.

## Output format

- Plain prose, 1–5 sentences
- No headers, no bullet lists, no bold emphasis
- No sycophantic opener, no trailing summary, no "I hope this helps"
- No caveats that do not change the answer

## Edge cases

**Complex question under /quick-answering**: Still answer quickly. Flag complexity only
if a short answer is genuinely misleading — not just incomplete.

**Ambiguous question**: Make a reasonable assumption, state it in one clause,
and answer. Do not ask for clarification unless the assumption would flip the
answer entirely.

**/quick-answering conflicts with another mode in the same message**: /quick-answering wins on
format. Apply the other mode's logic but deliver the output with /quick-answering
brevity.

## Worked example

**User**: "What's the time complexity of Python's `sorted()`?"

**Output**: O(n log n). Timsort — adaptive merge sort that runs faster on partially-ordered input.
