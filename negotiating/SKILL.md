---
name: negotiating
description: >
  Runs a structured negotiation prep and diagnosis pass — surfaces interests,
  BATNA, the counterpart's likely view, cognitive traps, opening and concession
  architecture, and a pre-mortem. Use when the user types /negotiating. Also
  trigger automatically (without being asked) whenever the user describes a
  real negotiation they are about to enter or are inside — salary, job offer,
  vendor or supplier deal, partnership, fundraise, buying or selling something
  significant, contract terms, dispute resolution, or any situation where two
  or more parties are working out terms and the user has skin in the game.
  Do NOT trigger for casual mentions of negotiation as a topic, for hypotheticals,
  or for academic questions about negotiation theory.
---

# /negotiating — Negotiation Prep & Diagnosis

Most negotiations are won or lost before the first word at the table. This skill
produces a structured prep pass that forces clarity on interests, alternatives,
and the counterpart's likely view — and stress-tests the user's plan against
the predictable ways it will go wrong.

The goal is not to make the user sound like a negotiation book. It is to make
them see the situation more clearly than their counterpart does.

## When to use this

- User explicitly types `/negotiating`
- User describes a real, upcoming or in-progress negotiation — even casually
  ("I have a salary call Thursday," "vendor wants to renew at +30%," "thinking
  about asking for equity")
- User asks for help with an offer, a counter, a walk-away decision, or a
  concession plan

Do NOT trigger on theoretical questions about negotiation, book-style requests,
or fictional scenarios — answer those directly without the workflow.

## Steps / Workflow

Copy this checklist and check off each step as you complete it:

```
Negotiation Prep Progress:
- [ ] Step 1: Situation diagnosis (type, real stakes, parties)
- [ ] Step 2: Interests, not positions (both sides, ranked)
- [ ] Step 3: BATNA and reservation point (user, counterpart, ZOPA, walk-away)
- [ ] Step 4: Cognitive trap check (one-two for user, one for counterpart)
- [ ] Step 5: Opening and concession architecture (anchor, axes, calibrated question)
- [ ] Step 6: Pre-mortem (most likely failure mode 6–18 months out)
- [ ] Step 7: Cross-cultural layer (only if relevant)
- [ ] Step 8: Ethics check (only if pressure point exists)
- [ ] Highest-leverage move in next 24 hours
```

Work through these in order. Skip any section that genuinely does not apply,
and say so in one line rather than padding.

### 1. Situation diagnosis (2–3 sentences)

Identify three things:
- **Type**: transactional vs. relational, one-shot vs. repeated, integrative
  potential vs. mostly distributive
- **Real stakes**: what actually happens to the user if no deal is reached —
  not the worst-case fantasy, the realistic outcome
- **Parties**: who is actually deciding, including the stakeholders not in the
  room (the boss, the spouse, the board, procurement, the regional office)

### 2. Interests, not positions

For both sides, list the underlying interests — *why* they want what they
want — ranked. Mark the user's one must-have and one nice-to-have explicitly.
For the counterpart, flag confidence: which interests are inferred vs. known.

End this section by naming where interests overlap (integrative potential —
trade space) and where they truly conflict (distributive — split-the-pie).

### 3. BATNA and reservation point

- User's BATNA — their best alternative if this deal collapses. If it is weak,
  the highest-leverage move is usually to improve it *before* negotiating, not
  to negotiate harder.
- Counterpart's likely BATNA — best inference, flagged as such.
- Rough ZOPA estimate where overlap likely exists.
- The user's walk-away number or condition, written down.

### 4. Cognitive trap check

Name the one or two biases most likely to bite *the user* in this specific
situation, and one likely affecting the *counterpart*. Examples to draw from:
anchoring, fixed-pie bias, escalation of commitment, reactive devaluation,
sunk cost, winner's curse, overconfidence in one's own BATNA.

This is not a textbook recital — pick the live ones.

### 5. Opening and concession architecture

- **First move**: anchor or let them anchor? Default rule: anchor when the user
  has better information about the deal's true value; let them anchor when they
  don't. State which applies and why.
- **Concession dimensions**: list 2–3 axes (price, scope, timeline, exclusivity,
  payment terms, etc.) ordered by what is cheap for the user and expensive for
  the counterpart. These are the trades that build value.
- **One calibrated question** to ask early — usually a "how" or "what" question
  that surfaces the counterpart's real constraint.

### 6. Pre-mortem (1–2 sentences)

Imagine the deal closes and goes badly 6–18 months later. What's the most
likely failure mode? If this is easy to write, the deal probably needs more
work before signing.

### 7. Cross-cultural layer (only if relevant)

If the counterpart is from a meaningfully different business culture from the
user, add a short diagnostic on five dimensions: hierarchy, time horizon,
trust-building speed, directness of communication, and whether the relationship
*is* the contract or supports it. Give one concrete behavioral adaptation.
Mark the diagnosis as a hypothesis to test in the first interaction, not a
verdict.

### 8. Ethics check (only if pressure point exists)

If the situation tempts manipulation (counterpart is desperate, asymmetric
information, vulnerable party), name it in one line and steer toward moves the
user would be comfortable with the counterpart later finding out about. Do not
moralize beyond that.

## Output format

- Lead with the diagnosis. No throat-clearing, no recap of what the user said.
- Use the section headers above only if the situation is complex enough to need
  them. For simple cases, prose is fine — match length to stakes.
- Every section should reference *specifics* from the user's situation. Generic
  advice that could apply to any negotiation is a failure mode of this skill.
- Label inferences about the counterpart as inferences. Do not assert what they
  want; reason about what they likely want and flag uncertainty.
- End with the single highest-leverage move the user can make in the next 24
  hours — usually about preparation, not tactics.
- No sycophantic opener, no trailing summary.

## Edge cases

**Mid-negotiation tactical question** ("they just countered at X, what do I
say?"): skip the full workflow. Answer the tactical question directly, but
quickly check whether the user has actually thought through interests and
BATNA — if not, surface that gap in one line.

**Debrief request** ("I just finished negotiating, here's what happened"):
flip the lens — what to learn, not what to do. Focus on what surprised them,
what they would do differently, what the outcome reveals about their model of
the counterpart.

**Coercive or abusive situation** (domestic, threats, illegal pressure):
do not apply the negotiation frame. Negotiation assumes two parties with
agency and legitimate interests. Suggest appropriate resources instead.

**Unethical request** (script for a deception, exploiting a vulnerable
counterpart): decline the specific ask, offer a legitimate version of the
underlying goal if one exists.

**User wants validation, not analysis**: if the user is clearly venting or
processing emotion about a negotiation that already happened, don't run the
workflow. Acknowledge first, offer the workflow as an option.

**Combined with /deciding** (when available): A natural sequence — run
`/deciding` on whether to negotiate at all (or which deal to take), then run
`/negotiating` on the chosen path. If `/deciding` is not in the available
skills list, mention to the user that decision-framework prep would normally
precede negotiation prep, and proceed with `/negotiating` standalone.

## Worked example (compact, mid-negotiation)

**User**: "Got an offer from Acme for $180k base. Asked for $200k. They came back with $185k. What now?"

**Output** (skipping the full 8-step prep, this is tactical mode per Edge cases):

- **Diagnosis**: They moved $5k. That is a low-effort hold pattern, not a real ceiling. Real ceilings sound like "this is the band for this level."
- **Inferred BATNA (counterpart)**: They have alternative candidates, but the gap-to-replace-you is at least three weeks of search — that's leverage you have without realizing it.
- **Cognitive trap on you**: anchoring. You have now mentally re-anchored on $185k as the new midpoint. Don't.
- **Move**: Counter at $195k tied to a non-cash dimension they care about (start date, signing-bonus structure, scope). Keep one calibrated question ready: "What would it take for you to get to my number?" Their answer reveals the real constraint — a band they can't break, a budget cycle, an internal precedent — and that's where the trade space actually opens.

*If full prep is needed before the next round, run the 8-step workflow on a fresh thread.*
