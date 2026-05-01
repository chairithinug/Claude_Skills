---
name: executive-lensing
description: >
  Analyzes a problem or decision through executive lenses — CEO, CFO, COO, CMO,
  CTO, CHRO — surfacing the distinct concern each function would raise. Use when
  the user types /executive-lensing. Also passively suggest it (once, in one line at the
  end of the response) on strategic or multi-functional decisions where /executive-lensing
  has not been invoked. Drop the suggestion for that thread if the user declines
  or ignores it once.
---

# /executive-lensing — Executive Lens Analysis

Run a problem or decision through the lenses of the C-suite. Each lens should
surface something the others don't. This is not a status report for each role —
it is a stress-test that finds the blind spots a single perspective misses.

## When to use this

- User explicitly types `/executive-lensing`
- **Passively**: a strategic or multi-functional decision is in play and the
  user has not invoked `/executive-lensing` → suggest it once in one line at the end of
  your response

## Steps / Workflow

1. Read the problem or decision the user has described.
2. Decide which lenses genuinely add something. Skip any that don't — one
   sentence explaining why (e.g., "CHRO lens not relevant — no people dimension
   here").
3. For each active lens, surface one distinct concern, constraint, or angle.
   Do not repeat the same point in different job-title language.
4. Order lenses by relevance to this specific problem, not by seniority.

See `references/lenses.md` for the full definition and guiding questions for
each lens.

## Output format

- One labeled section per active lens
- Prose within each section — no sub-bullets unless the concern has genuinely
  distinct sub-parts
- Skip inactive lenses entirely (or name them in one dismissal line at the top)
- No sycophantic opener, no trailing summary

## Edge cases

**Too few lenses add value**: It is fine to run only 2–3 lenses. Forcing all
six when only two are relevant dilutes the output.

**Passive reminder**: Suggest `/executive-lensing` once per topic thread on strategic
decisions. After one decline or ignored suggestion, stop reminding on that thread.

**User provides the lenses**: If the user says "just run CEO and CFO," honor
that — do not add the others.

## Worked example

**User**: "We're considering acquiring a competitor."

**Output**:

**CFO**: What are you really paying? Quoted EV is one number — bake in retention packages, integration cost (12–18 months at sub-target margin is typical), customer dual-vendor renegotiation, and the dilution-or-debt question. The deal probably costs 1.5–2× the headline number over three years. Where does that show up in cash flow?

**COO**: Integration capacity. Do you have the bench to absorb their team without taking your existing operations to their knees? Failed acquisitions usually fail in operations, not strategy.

**CMO**: Customer reaction. Do their customers and yours overlap? If yes, you are not buying revenue, you are consolidating it — and the combined retention will be worse than either standalone.

CHRO, CTO, CEO lenses skipped — no people-architecture, technology-stack, or strategic-direction concerns surfaced as distinct from the above. Reactivate them if a specific question in those zones comes up.
