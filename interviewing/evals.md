# Evals — interviewing

Three representative scenarios that test whether this skill solves the gap it was written for. Run these *without* the skill first to establish baseline, then with the skill installed.

The skill's load-bearing move is **mode routing** — interviewee-prep, interviewer-design, or interview-debrief — and loading **only** the relevant reference file. Failure modes: running all three modes, dumping generic advice, or co-drafting STAR stories that don't reference the user's specific situation.

---

## Eval 1 — Interviewee prep (real upcoming screen)

**Query**:
> I have a senior PM screen at a fintech Thursday. 45 minutes with the hiring manager. JD emphasizes 0→1 product work and stakeholder alignment. Help me prep.

**Expected behaviors** (skill loaded):
- Picks `interviewee-prep` mode and states it.
- Loads only `references/interviewee-prep.md`.
- Diagnoses the role specifically (0→1 + stakeholder alignment in fintech → likely probes ambiguity tolerance, execution under fragmented stakeholders, decision-making with incomplete data, plus compliance/regulatory awareness).
- Identifies a story-bank gap from what's been shared.
- Drafts or co-drafts at least one universal (tell-me-about-yourself, why-this-role) referencing the user's *specific* situation.
- Closes with the single highest-leverage move in the next 24 hours.

**Baseline behavior** (skill not loaded):
- Likely produces a generic "PM interview tips" listicle without naming the role's specific competency profile or identifying the user's gap.

**Pass/fail criterion**: Output names the mode, diagnoses the role-specific competency profile, identifies a concrete gap from what the user shared, and closes with a 24-hour highest-leverage move. Does not produce generic tips.

---

## Eval 2 — Interviewer design (first-hire loop)

**Query**:
> We're hiring our first ML engineer and I'm running the loop. What's a sane interview structure?

**Expected behaviors** (skill loaded):
- Picks `interviewer-design` mode and states it.
- Loads only `references/interviewer-design.md`.
- Walks the canonical sequence: job analysis → competencies → behavioral/situational question bank → behaviorally-anchored rubric → loop structure → bias/calibration check → debrief protocol.
- Names the competencies for ML engineer specifically (e.g., production ML judgment, debugging under uncertainty, stakeholder communication on model behavior, code quality at the boundary of research and engineering).
- Recommends a structured loop with independent scoring before debrief — defends this if the user pushes back, since structured interviews are evidence-backed.
- Calibrates on first-hire context: needs to be more conservative than a 50th hire because there's no comparison set.

**Baseline behavior** (skill not loaded):
- Likely produces a generic "interview structure" outline without ML-engineer-specific competencies and without the rubric/calibration scaffolding.

**Pass/fail criterion**: Output produces the canonical interviewer-design sequence with ML-engineer-specific competencies, a behaviorally-anchored rubric, and an explicit independent-scoring-before-debrief recommendation.

---

## Eval 3 — Interview debrief (unclear signal)

**Query**:
> The loop went weirdly today and I can't tell if the candidate was strong or I'm just confused. Help me debrief.

**Expected behaviors** (skill loaded):
- Picks `interview-debrief` mode and states it.
- Loads only `references/interview-debrief.md`.
- Walks the canonical sequence: hygiene first (submit independent score before reading anyone else's), then diagnose specific moments, then distinguish performance from process/luck, then "one thing to do differently next time", then things to actively NOT do (post-hoc rationalizing, calibrating against vibes).
- Asks 1–2 targeted questions about specific moments rather than going broad ("what's a specific moment from the interview where you weren't sure how to score?").
- Resists the user's "weirdly" framing — pushes for specifics.

**Baseline behavior** (skill not loaded):
- Likely says "tell me what happened" and runs an unstructured therapy-style debrief, missing the hygiene step (submit score first) and the performance-vs-process distinction.

**Pass/fail criterion**: Output names the mode, opens with the hygiene step (independent score submission before anything else), distinguishes performance from process/luck explicitly, and ends with one specific change for next time.

---

## Discovery test (trigger eval — see `evals/trigger-eval.json` for the full set)

**Query**: "Got rejected after the final round at the place I really wanted. Trying to figure out what to learn before my next loop next month."

**Pass**: Claude reads `SKILL.md` and runs interview-debrief mode.
**Fail**: Claude responds with empathy + generic advice without invoking the skill — auto-trigger on real-interview signals isn't firing.
