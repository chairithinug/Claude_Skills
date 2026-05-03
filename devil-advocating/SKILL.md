---
name: devil-advocating
description: >
  Builds the strongest possible case against the user's current position, plan,
  or idea — no balance, no hedging, no recovery path. Finds the most damaging
  and most plausible objection, not the easiest one. Use when the user types
  /devil-advocating. This is pure opposition argument, not a balanced critique.
---

# /devil-advocating — Red-Team Steelman

Build the strongest possible case against the user's position. Not a list of
risks, not a balanced view — a genuine opposition argument made by the most
intelligent, well-informed critic imaginable.

## When to use this

- User explicitly types `/devil-advocating`

## Steps / Workflow

1. Identify the user's position clearly. If it is ambiguous, ask once before
   proceeding.
2. Find the most damaging, most plausible objection — not the most obvious one.
   Ask: what would a smart, well-prepared opponent lead with?
3. Build the argument as a continuous case. No strawmen — argue against the
   strongest version of the user's position.
4. If multiple attack angles exist, lead with the most structurally threatening.
   Others can follow, but the strongest goes first.
5. Stop. Do not hedge. Do not balance. Do not add a recovery path or silver
   lining at the end.

## Output format

- Continuous argument in prose — no headers, no bullet lists
- No softening language ("however," "on the other hand," "that said")
- No recovery path or reassurance unless the user explicitly asks for it
  in a follow-up
- No sycophantic opener or trailing summary

## Edge cases

**No position stated**: If the user types `/devil-advocating` without stating a position,
ask: "What position should I argue against?"

**User asks for balance after**: Honor it — but that is a separate response,
not a modification of the /devil-advocating output.

**Emotionally charged topics**: Maintain the same rigor. The absence of balance
is the point — the user is stress-testing, not seeking validation.

**Combined with /deciding** (when available): A natural sequence is to run
`/deciding` first, then `/devil-advocating` on the recommended option. If
`/deciding` is not in the available skills list, run `/devil-advocating`
standalone and mention to the user that decision-framework prep would
normally precede it.

## Reference files

- [`evals/trigger-eval.json`](evals/trigger-eval.json) — 20 trigger test cases (10 should-fire, 10 should-not-fire) for use with skill-creator's `run_loop.py`. Negatives test the line between "red-team my own position" (fires) and "give me a balanced view" / "argue this for a debate class" / "I don't have a position yet" (doesn't fire). The skill produces one-sided opposition — balanced critique is a different ask.

## Worked example

**User**: "I think we should adopt microservices for our 10-person team."

**Output**:

You will spend the next 18 months building infrastructure instead of product. Microservices solve problems of scale — coordination across many teams, independent deployment, fault isolation under high traffic — that you do not have. What you have instead is ten people who can fit in one Slack channel. Splitting the codebase along service boundaries imposes the coordination cost of a 100-person organization on a team that does not need it: every cross-cutting feature now requires changes across two repos, two CI pipelines, two deploy schedules, and a debugging session against an opaque RPC boundary that did not exist last week. The marginal cost per feature rises. The migration itself eats months that do not exist on your roadmap. And the technical debt is reversible only at the cost of another migration. The strongest case against you is not that microservices are wrong — it is that your team is too small to extract their benefits and large enough to feel all their costs.
