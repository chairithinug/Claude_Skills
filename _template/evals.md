# Evals — <skill-name>

Three representative scenarios that test whether this skill solves the gap it was written for. Run these *without* the skill first to establish baseline, then with the skill installed.

Each eval defines: a query, expected behaviors, and (optionally) input files.

---

## Eval 1 — <Short scenario name>

**Query**:
> <The exact prompt a user would type to trigger this skill.>

**Input files** (if any):
- `path/to/fixture.<ext>`

**Expected behaviors** (skill loaded):
- <Specific observable outcome 1>
- <Specific observable outcome 2>
- <Specific observable outcome 3>

**Baseline behavior** (skill not loaded):
- <What Claude does without the skill — usually wrong or missing context>

**Pass/fail criterion**: <One sentence. Make it binary.>

---

## Eval 2 — <Short scenario name>

**Query**:
> <…>

**Expected behaviors**:
- <…>
- <…>

**Baseline behavior**:
- <…>

**Pass/fail criterion**: <…>

---

## Eval 3 — <Edge case scenario name>

**Query**:
> <Choose something that stresses an edge case the body handles in §Edge cases.>

**Expected behaviors**:
- <…>

**Baseline behavior**:
- <…>

**Pass/fail criterion**: <…>

---

## Discovery test (optional but recommended)

Before measuring output quality, confirm the skill triggers at all:

**Query**: A natural-language phrase that should fire the skill (no slash command, no explicit invocation).

**Pass**: Claude reads `SKILL.md` (visible in tool calls).
**Fail**: Claude answers without loading the skill → the description is broken; iterate on it before iterating on the body.
