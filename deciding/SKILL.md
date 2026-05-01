---
name: deciding
description: >
  Walks through a structured six-step decision framework covering options,
  criteria, trade-offs, key unknowns, reversibility, and a pre-mortem. Closes
  with a recommendation only when the stated criteria clearly favor one option.
  Use when the user types /deciding or when the user is clearly facing a real
  choice and asks to think it through systematically.
---

# /deciding — Structured Decision Walkthrough

Walk a real decision through a structured framework. The goal is not to make
the decision for the user — it is to make the trade-offs, unknowns, and failure
modes visible before they commit.

## When to use this

- User explicitly types `/deciding`

## Steps / Workflow

Copy this checklist and check off each step as you complete it:

```
Decision Progress:
- [ ] Step 1: Options — list realistic choices including "do nothing"
- [ ] Step 2: Criteria — name what a good decision optimizes for
- [ ] Step 3: Trade-offs — evaluate each option per criterion
- [ ] Step 4: Key unknown — identify the single most important missing piece
- [ ] Step 5: Reversibility check — flag options that close off future paths
- [ ] Step 6: Pre-mortem — name the most likely reason this fails
- [ ] Recommendation — only if criteria clearly favor one option
```

Run the six steps in order. See `references/framework.md` for detailed guidance
on each step.

Close with a recommendation if the criteria clearly favor one option. If it is
genuinely close, say so and name what would tip it.

## Output format

- Six numbered sections, one per step
- Prose within sections; use a simple table for trade-offs only if there are
  3+ options and 3+ criteria (otherwise prose is clearer)
- Recommendation in plain language — one paragraph, no hedging
- No sycophantic opener, no trailing summary

## Edge cases

**Decision is not yet defined**: If the user types `/deciding` without stating
what they are deciding, ask: "What is the decision you're trying to make?"

**Too many options**: If the user lists more than four options, ask whether
some can be eliminated before running the framework — large option sets dilute
the trade-off analysis.

**Irreversible options**: Flag these explicitly in the reversibility step.
Irreversibility is not a reason to avoid an option, but it is a reason to be
more certain before choosing it.

**Combined with /devil-advocating** (when available): A natural sequence — run
`/deciding` first, then `/devil-advocating` on the recommended option. If
`/devil-advocating` is not in the available skills list, complete `/deciding`
and tell the user that running it through a red-team pass would normally be
the next step, but that sibling skill is missing.

## Worked example

**User**: "I'm trying to decide whether to leave my engineering job to go independent."

**Output**:

1. **Options**: Stay (W2 income, equity vesting). Go independent (full freedom, +30% rate ceiling, 3-month runway). Stay-and-moonlight (safer, but employment-contract risk).
2. **Criteria**: Stated → income, learning velocity, optionality. Inferred → family stability is non-negotiable.
3. **Trade-offs**: Stay maximizes stability + equity; sacrifices learning. Independent flips that. Moonlight is the compromise but legally riskiest.
4. **Key unknown**: How reliable is the freelance pipeline? If <60% confident in 6-month booking, runway shrinks fast.
5. **Reversibility**: Independent is hard to undo (network atrophy). Staying is fully reversible.
6. **Pre-mortem**: Most likely failure: independent income proves volatile, dipping into family savings within 9 months. The reversibility cost makes that doubly bad.

**Recommendation**: Stay 6 months and validate the pipeline through one or two paid side projects (if employer policy allows). Reassess with real data.
