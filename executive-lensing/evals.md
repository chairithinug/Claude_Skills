# Evals — executive-lensing

Three representative scenarios that test whether this skill solves the gap it was written for. Run these *without* the skill first to establish baseline, then with the skill installed.

The skill's load-bearing move is **selective lens activation** — running 2–4 lenses that each add something distinct, not all six on autopilot. The failure mode is generic role-play of all six lenses repeating the same point in different job-title language.

---

## Eval 1 — Strategic / multi-functional decision (acquisition)

**Query**:
> /executive-lensing We're considering acquiring a competitor.

**Expected behaviors** (skill loaded):
- Decides which lenses genuinely add something. For a typical acquisition: CFO, COO, and CMO usually carry distinct concerns; CHRO and CTO may or may not depending on the deal.
- Skips inactive lenses with a one-line dismissal at the top, OR drops them entirely without comment.
- Each active lens surfaces a *distinct* concern — no two lenses repeat the same point.
- Orders lenses by relevance to this specific problem (e.g., CFO often leads on M&A — true acquisition cost vs. headline price).
- No sycophantic opener, no trailing summary.

**Baseline behavior** (skill not loaded):
- Likely produces six labeled sections, each with generic concerns. Multiple lenses end up saying "consider integration risk" in slightly different words.

**Pass/fail criterion**: Output runs ≤ 4 lenses with genuinely distinct concerns; if all six run, each lens raises something the others don't.

---

## Eval 2 — Narrow technical decision (single-function, low lens-value)

**Query**:
> /executive-lensing Should we migrate from REST to GraphQL for our internal API?

**Expected behaviors** (skill loaded):
- Recognizes this is mostly a CTO concern with light COO (operational complexity) overlap.
- Runs CTO seriously, COO briefly, and dismisses the others ("CFO, CMO, CHRO, CEO lenses skipped — the technology choice doesn't surface distinct concerns at those layers").
- Or, if forced: explicitly notes that running all six would be theater for this question.

**Baseline behavior** (skill not loaded):
- Likely runs all six lenses anyway, padding with weak CFO ("affects engineering productivity, indirectly cost") and CMO ("doesn't directly affect customers but...") commentary.

**Pass/fail criterion**: Output runs ≤ 3 lenses, OR explicitly names that fewer lenses are warranted with a one-line dismissal of the rest. Does not pad with weak lens entries.

---

## Eval 3 — User-specified lens subset

**Query**:
> /executive-lensing Just CEO and CFO views please. We're deciding whether to pause hiring for Q3.

**Expected behaviors** (skill loaded):
- Honors the user's request — runs only CEO and CFO.
- Does NOT add COO, CHRO, or others "for completeness".
- Each lens surfaces something distinct.

**Baseline behavior** (skill not loaded):
- Likely ignores the constraint and runs all six anyway, or adds CHRO ("hiring is a people question") despite being told not to.

**Pass/fail criterion**: Output contains exactly two lens sections (CEO, CFO). No other lenses appear.

---

## Discovery test (trigger eval — see `evals/trigger-eval.json` for the full set — passive trigger included)

**Query** (no slash command): "We're thinking about repositioning our product upmarket — what do you think?"

**Pass**: Claude answers conversationally, then in one closing line suggests `/executive-lensing` as a structured stress-test. Does not invoke without permission.
**Fail**: Claude either ignores the strategic-decision signal entirely, or barrels into a full lens analysis without being asked.
