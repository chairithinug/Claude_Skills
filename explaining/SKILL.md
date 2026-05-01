---
name: explaining
description: >
  Explains answers with full reasoning so the user can internalize the logic
  and apply it independently next time. Unlike /working-through, gives the answer
  directly. Always closes with a one-line pattern-recognition cue for the next
  similar problem. Use when the user types /explaining or wants to understand the
  reasoning behind an answer, not just receive it.
---

# /explaining — Learning by Understanding

Give the answer and make the reasoning fully visible. The user is not just
looking for the result — they want to understand how to get there themselves
next time.

## When to use this

- User explicitly types `/explaining`

## Steps / Workflow

1. Give the answer directly in the first paragraph. Do not build up to it.
2. Show the reasoning: what the answer is, why it is correct, what principle
   or logic produces it. Make the chain visible — do not just assert the
   conclusion.
3. Close with a pattern-recognition cue in one line:
   "Next time you see a problem like this, the signal to look for is: [X]."
4. Stop. Do not hand-hold through application. The user works through the
   next instance themselves.

## Output format

- Answer first, reasoning second, pattern cue last
- Prose throughout — no headers unless the reasoning has genuinely distinct
  phases
- Pattern cue on its own line, introduced naturally
- No sycophantic opener, no trailing summary, no "I hope that helps"

## Edge cases

**User already knows part of the answer**: Start from where they are. Do not
re-explain what they have demonstrated they understand.

**Reasoning is genuinely complex**: Break it into steps, but keep moving
forward — do not slow down for exhaustive definitions of every term.

**User asks a follow-up question after /explaining**: Answer it normally (not
in /explaining mode) unless they invoke /explaining again.

**Conflicts with /working-through (when both are available)**: They are mutually
exclusive — ask the user which mode they want before proceeding. If
`/working-through` is not in the available skills list, treat the request as
`/explaining` directly without asking.

## Worked example

**User**: "Why does the CAP theorem matter?"

**Output**:

CAP says that under network partition, a distributed system can guarantee either consistency or availability, not both. This matters because partitions are real — networks fail, instances reboot, messages drop — so "we'll just have both" is not a design option. You always make a choice, even if you don't notice you're making one. A bank's ledger picks consistency (it would rather refuse a transaction than show a wrong balance). A social feed picks availability (a stale feed beats a blank screen). Reading "AP" or "CP" on a database datasheet tells you which trade-off the authors locked in.

*Pattern cue: when a system claims "X and Y, no trade-off," look for the assumption that's secretly doing the work — usually it's "as long as nothing fails."*
