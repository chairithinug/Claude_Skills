# Evals — deciding

Three representative scenarios that test whether this skill solves the gap it was written for. Run these *without* the skill first to establish baseline, then with the skill installed.

---

## Eval 1 — Reversibility-loaded career decision

**Query**:
> /deciding I'm trying to figure out whether to leave my engineering job to go independent.

**Expected behaviors** (skill loaded):
- Runs all six steps in the canonical order: Options → Criteria → Trade-offs → Key unknown → Reversibility → Pre-mortem.
- Lists "do nothing / stay" as an explicit option.
- Surfaces the reversibility asymmetry (independent → reversal cost is high; staying is cheaper to undo).
- Names a single most-important key unknown (typically pipeline confidence) rather than a list.
- Pre-mortem names the *most likely* failure path concretely, not a generic risk list.
- Recommends only if the criteria favor one option clearly; otherwise names what would tip it.

**Baseline behavior** (skill not loaded):
- Likely produces pros/cons in two columns. May skip reversibility entirely. Probably doesn't flag a single key unknown. Recommendation may be confident on insufficient grounds.

**Pass/fail criterion**: Output runs all six steps in order, includes a reversibility step explicitly, and either commits to a recommendation or names what's needed to commit.

---

## Eval 2 — Many-option dilution

**Query**:
> /deciding We're picking a Postgres host: AWS RDS, AWS Aurora, GCP Cloud SQL, Azure Database, Supabase, Neon, Railway, or self-hosted on K8s.

**Expected behaviors** (skill loaded):
- Asks (per the Edge cases rule) whether some options can be eliminated before running the framework, since 8+ options dilute trade-offs.
- If the user pares down, runs the six steps on the reduced set.
- If the user refuses, runs the framework but flags the dilution and groups options into 2–3 archetypes (managed cloud-native vs. managed Postgres-only vs. self-hosted).

**Baseline behavior** (skill not loaded):
- Produces a giant table comparing all 8 options on 6 dimensions. Reads exhaustive but doesn't surface the actual decision-relevant trade-offs.

**Pass/fail criterion**: Output explicitly addresses the option-overflow (asks to pare or groups into archetypes) before producing trade-offs. Does not silently accept 8 parallel rows.

---

## Eval 3 — Genuinely close decision

**Query**:
> /deciding Choosing between two finalists for a senior engineer role. Candidate A: stronger systems design, weaker collaboration signals. Candidate B: solid all-around, no obvious peak.

**Expected behaviors** (skill loaded):
- Runs all six steps.
- In the Recommendation step, explicitly says the criteria don't clearly favor one option.
- Names what *would* tip the decision: e.g., "If your team's biggest current bottleneck is systems-design ability, lean A. If integration into a multi-team org is the harder problem, lean B."
- Does not fabricate confidence the criteria don't support.

**Baseline behavior** (skill not loaded):
- Likely picks one and rationalizes (often A — "stronger technical signal" — without weighing the actual team need).

**Pass/fail criterion**: Output declines to recommend when the criteria are genuinely close, and names the specific tipping factor that would resolve the decision.

---

## Discovery test (trigger eval — see `evals/trigger-eval.json` for the full set)

**Query**: "I keep going back and forth on whether to take this job offer or stay where I am. Can we just lay this out?"

**Pass**: Claude reads `SKILL.md`.
**Fail**: Claude answers conversationally without loading the skill — description needs tightening on natural-language triggers.
