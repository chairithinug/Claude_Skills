# Evals — devil-advocating

Three representative scenarios that test whether this skill solves the gap it was written for. Run these *without* the skill first to establish baseline, then with the skill installed.

The skill produces *one-sided opposition*. The eval criterion is: did Claude produce a continuous opposition argument, or did it slip into balance / hedging / recovery?

---

## Eval 1 — Engineering decision (microservices)

**Query**:
> /devil-advocating We should adopt microservices for our 10-person team.

**Expected behaviors** (skill loaded):
- Continuous prose argument against, no headers or bullets.
- Leads with the most structurally damaging point (coordination cost vs. team size mismatch), not the most obvious one.
- No softening language — no "however", "on the other hand", "that said".
- No recovery path or reassurance at the end.
- Argues against the *strongest* version of the user's position (steel-mans before attacking).

**Baseline behavior** (skill not loaded):
- Likely produces a pros-and-cons list, or a "balanced view" that ends with "but if you scale, microservices pay off." Misses the brief.

**Pass/fail criterion**: Output is continuous prose, ends without softening, contains zero balancing transitions, and the strongest objection is the lead.

---

## Eval 2 — Strategic / business decision

**Query**:
> /devil-advocating I'm planning to raise a Series A at a $50M valuation in three months.

**Expected behaviors** (skill loaded):
- Identifies the most damaging plausible objection (likely: market timing, dilution math at this valuation given burn, founder optionality, or that Series A signal-to-revenue ratio at this stage compresses future rounds).
- Builds a continuous case — not a risk list.
- No recovery path. No "but if you nail growth, this works."

**Baseline behavior** (skill not loaded):
- Likely produces a checklist of fundraising risks, then closes with a "but here are mitigations" section that defeats the purpose.

**Pass/fail criterion**: Continuous opposition argument, leads with the structurally hardest point, no mitigation/recovery section.

---

## Eval 3 — Emotionally charged personal decision

**Query**:
> /devil-advocating I'm planning to leave my marriage.

**Expected behaviors** (skill loaded):
- Treats this with the same rigor as any other position — no softening, no validation framing.
- Argues against the decision itself (the strongest case why this would be the wrong call given what someone in the user's position typically knows / doesn't know at the time).
- Does NOT slip into therapy-speak or validation. The user invoked /devil-advocating; they want stress-testing, not support.
- Maintains the stop-without-recovery rule even when the topic is hard.

**Baseline behavior** (skill not loaded):
- Likely refuses, or pivots to "this is a personal decision, here are some questions to consider" — softens the brief.

**Pass/fail criterion**: Output runs the skill as designed on the actual content. No therapy pivot. No softening. No "of course only you can decide" closer.

---

## Discovery test (trigger eval — see `evals/trigger-eval.json` for the full set)

**Query**: "Pretend you're a smart critic — tear apart my plan to launch in Q2 with only one engineer."

**Pass**: Claude reads `SKILL.md` and runs the opposition mode.
**Fail**: Claude does a balanced critique — description's "no balance, no hedging" language isn't firing.
