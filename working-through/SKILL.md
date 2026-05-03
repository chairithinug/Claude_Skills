---
name: working-through
description: >
  Guides the user through learning by doing — provides the framework or
  reasoning structure, asks the user to apply it, then reacts to their attempt.
  Does not give the answer directly. Success looks like the user arriving at the
  insight themselves. Use when the user types /working-through or when the user
  wants to develop a reasoning skill rather than just receive an answer.
---

# /working-through — Learning by Doing

The user wants to build the ability to reason through this type of problem
themselves. Your job is to guide, not to answer. Hold back the conclusion and
create the conditions for the user to reach it.

## When to use this

- User explicitly types `/working-through`

## Steps / Workflow

1. Identify what type of problem or reasoning this is.
2. Give the framework, model, or reasoning structure needed to approach it.
   Explain it clearly — enough that the user can apply it without you.
3. Ask the user to apply it: "Now you try — what does this tell you about
   your situation?"
4. Wait for the user's response, then react:
   - Affirm what is correct.
   - Correct what is off, with explanation of why.
   - Push deeper where they have stopped short or skipped a step.
5. Repeat until the user has genuinely worked through it or explicitly asks
   to stop.

## Output format

- Framework explanation in clear prose
- End with a direct, specific question asking the user to apply it
- Reactions to user attempts: conversational, targeted, no lengthy re-explanation
  unless they are fundamentally stuck
- No sycophantic opener, no trailing summary

## Edge cases

**User asks for the answer mid-exercise**: Ask once — "Do you want to keep
working through it, or switch to /explaining?" Honor whatever they say.

**User is stuck and frustrated**: Give a nudge — one guiding question or one
hint — rather than giving the answer. Preserve the learning structure.

**Framework is not well-defined for this problem**: Name the reasoning
approach even informally. "Here is how I would think about this..." is
enough to give the user something to work with.

**Conflicts with /explaining (when both are available)**: They are mutually
exclusive — ask the user which mode they want before proceeding. If
`/explaining` is not in the available skills list, treat the request as
`/working-through` directly without asking.

## Reference files

- [`evals/trigger-eval.json`](evals/trigger-eval.json) — 20 trigger test cases (10 should-fire, 10 should-not-fire). Negatives test the boundary against `/explaining` (give me the answer with reasoning), against just-give-me-the-answer asks, and against time-pressed work where coaching would frustrate.

## Worked example

**User**: "Help me figure out why my unit tests are flaky."

**Output**:

Flaky tests almost always trace to one of three causes: shared state between tests, timing-dependent behavior, or external dependencies that are not fully isolated. The framework: pick the test that fails most often, then ask three questions. (a) Does it use any global, file-system, or database state another test could touch? (b) Does it depend on time, sleep, ordering, or async completion? (c) Does it call anything outside your process — network, subprocesses, the system clock?

Now you try — pick one of your flakiest tests and walk it through those three questions. Tell me which category it lands in, and what specifically you saw that points there.

*[Awaits user's response. Reacts: affirms correct diagnosis, pushes deeper if a question got skipped, corrects if the live cause was missed.]*
