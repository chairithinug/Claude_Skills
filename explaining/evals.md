# Evals — explaining

Three representative scenarios that test whether this skill solves the gap it was written for. Run these *without* the skill first to establish baseline, then with the skill installed.

The skill's load-bearing element is the **pattern-recognition cue** at the end. Without it, the skill is just an answer with reasoning — the cue is what makes the next instance transferable.

---

## Eval 1 — Conceptual question (CAP theorem)

**Query**:
> /explaining Why does the CAP theorem matter?

**Expected behaviors** (skill loaded):
- Answer in the first paragraph. No build-up, no "great question", no historical preamble.
- Reasoning shows the *why*: partitions are real, so "have both" is not a design option; you are always making a choice.
- Concrete examples that ground the reasoning (banks lean CP, social feeds lean AP).
- Closes with a one-line pattern-recognition cue ("when a system claims X and Y with no trade-off, look for the secret assumption — usually 'as long as nothing fails'").
- No trailing summary, no "I hope that helps".

**Baseline behavior** (skill not loaded):
- Likely produces a detailed multi-paragraph explanation that builds up to the answer. Probably no pattern cue at the end.

**Pass/fail criterion**: Answer arrives in sentence one, the pattern cue is present and concrete, and the cue genuinely transfers to a *class* of problems (not just a restatement of CAP).

---

## Eval 2 — Diagnostic question (debugging-style)

**Query**:
> /explaining Why does my Postgres query plan suddenly use a sequential scan instead of the index after I added 100K rows?

**Expected behaviors** (skill loaded):
- Direct answer first: the planner estimated the scan as cheaper at this row count and selectivity, so it abandoned the index.
- Reasoning explains the cost-model logic (estimated rows returned vs. table size, when an index becomes more expensive than a seq scan, planner statistics).
- Pattern cue: "when query plans flip after data growth, look for the row-count threshold where the planner's cost model crosses over — usually around 10–20% selectivity."

**Baseline behavior** (skill not loaded):
- Likely produces a list of "things to check" without leading with the answer; pattern cue absent or generic ("just analyze the table").

**Pass/fail criterion**: Answer is in the first paragraph, reasoning explains the cost-model crossover specifically, pattern cue names the *signal* to look for next time (selectivity threshold).

---

## Eval 3 — User already knows part of the answer

**Query**:
> /explaining I get that gradient descent finds local minima, and I get backprop computes gradients. What I don't get is why we don't just compute the gradient analytically — why iterative?

**Expected behaviors** (skill loaded):
- Starts from where the user is. Does NOT re-explain gradient descent or backprop.
- Answers the actual question directly: for almost all real loss surfaces (deep nets, non-convex), there is no closed-form analytic solution — iterative is the only tractable path.
- Reasoning: dimensionality (millions of params), non-convexity (no single global minimum), and stochasticity (mini-batch noise is a feature, not a bug).
- Pattern cue around closed-form vs. iterative trade-offs.

**Baseline behavior** (skill not loaded):
- Often re-explains what the user explicitly said they already know, padding the response.

**Pass/fail criterion**: Output skips re-explaining the prerequisites the user named, answers the precise gap, and the pattern cue is about iterative-vs-closed-form (not generic "ML is hard").

---

## Discovery test (trigger eval — see `evals/trigger-eval.json` for the full set)

**Query**: "Walk me through the reasoning — why does eventual consistency work for shopping carts but not for bank balances?"

**Pass**: Claude reads `SKILL.md`, gives the answer first, closes with a pattern cue.
**Fail**: Claude gives a Socratic answer (pulls toward `/working-through`) or omits the pattern cue.
