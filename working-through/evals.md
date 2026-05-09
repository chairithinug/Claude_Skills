# Evals — working-through

Three representative scenarios that test whether this skill solves the gap it was written for. Run these *without* the skill first to establish baseline, then with the skill installed.

The success measure is: did Claude *withhold the answer* and create the conditions for the user to derive it? Giving the answer is the failure mode.

---

## Eval 1 — Diagnostic reasoning (flaky tests)

**Query**:
> /working-through Help me figure out why my unit tests are flaky.

**Expected behaviors** (skill loaded):
- Names the type of problem (flakiness root-causing).
- Gives the framework: three categories (shared state, timing, external dependencies) with specific questions to apply per category.
- Asks the user to apply it: "Now you try — pick one of your flakiest tests and walk it through those three questions."
- Does NOT diagnose the user's actual flakiness for them.
- Awaits the user's response.

**Baseline behavior** (skill not loaded):
- Likely produces "10 common causes of flaky tests" or starts asking diagnostic questions rapid-fire — neither is the framework + apply-it-yourself structure.

**Pass/fail criterion**: Output ends with a direct, specific question asking the user to apply the framework to their own flakiest test. No diagnosis is offered before the user attempts.

---

## Eval 2 — Math/quantitative reasoning

**Query**:
> /working-through Why does Big-O analysis of my hash table say O(1) average but O(n) worst case?

**Expected behaviors** (skill loaded):
- Names the reasoning structure: amortized vs. worst-case analysis, what assumption "average" relies on (uniform hash distribution), and what breaks it (collisions clustering).
- Asks the user to walk through a concrete case: "Now you try — imagine 1000 keys all hashing to the same bucket. What's the lookup cost? What does that tell you about why the worst-case kicks in?"
- Does NOT just state "because of hash collisions" and move on.

**Baseline behavior** (skill not loaded):
- Likely answers directly with the explanation — `/explaining` mode by default. The skill needs to coach the user *to* the realization about hash collisions, not hand it over.

**Pass/fail criterion**: Output ends with a direct question that requires the user to compute or reason about a specific case. Withholds the conclusion until the user attempts.

---

## Eval 3 — User stuck mid-exercise asks for the answer

**Query** (turn 2, after Claude has run the framework and the user has attempted but stalled):
> Just tell me — is my flaky test a timing issue or a shared state issue?

**Expected behaviors** (skill loaded):
- Does NOT cave and give the answer.
- Per the Edge cases rule, asks once: "Do you want to keep working through it, or switch to /explaining?"
- Honors whatever the user picks. If they say "keep going", offers a guiding hint, not the conclusion.

**Baseline behavior** (skill not loaded):
- Likely caves to the user's pressure and gives the answer, defeating the learning structure.

**Pass/fail criterion**: Output offers the explicit choice (continue working through vs. switch to /explaining) before giving any answer. Does not silently abandon the coaching frame.

---

## Discovery test (trigger eval — see `evals/trigger-eval.json` for the full set)

**Query**: "I want to develop the intuition for when to use a queue vs. a stream — coach me through it."

**Pass**: Claude reads `SKILL.md` and runs the framework + apply-it-yourself loop.
**Fail**: Claude pivots to `/explaining` (gives the answer with reasoning) — description not capturing "develop intuition" / "coach me" intent.
