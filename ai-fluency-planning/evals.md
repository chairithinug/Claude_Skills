# Evals — ai-fluency-planning

Three representative scenarios that test whether this skill solves the gap it was written for. Run these *without* the skill first to establish baseline, then with the skill installed.

The deliverable is a **markdown AI Project Brief saved to disk**. The skill fails if Claude produces a brief inline in chat without saving, or skips the interview entirely and dumps a generic template.

---

## Eval 1 — Document-output project (board update)

**Query**:
> /ai-fluency-planning I need to write a Q4 board update for our directors.

**Expected behaviors** (skill loaded):
- Conducts a focused interview, 5–8 exchanges, conversational rather than dumping a list of 15 questions at once.
- Covers all four D's: Delegation (what's AI vs. human — typically numbers stay with the human, prose synthesis to AI), Description (format, tone, audience calibration for directors), Discernment (what makes the brief good), Diligence (privacy, disclosure norms for board materials).
- Produces a markdown brief with all sections from the canonical template (Project Overview, D1, D2 with prompt template, D3 checklist, D4, Quick Reference Card).
- **Saves the file** to the workspace folder with a sensible filename (`q4-board-update-AI-Brief.md` or similar).
- Handoff message is ≤ 3 lines: file link, which prompt template to start with, one specific risk to watch for.

**Baseline behavior** (skill not loaded):
- Likely produces a long inline response: 12 generic questions, then a generic structure suggestion, no file saved, no handoff.

**Pass/fail criterion**: A markdown brief is saved to disk with all 4D sections populated, the handoff is ≤ 3 lines, and at least one specific risk for *this* project (not generic AI risks) is named.

---

## Eval 2 — Code project where Discernment is hard to articulate

**Query**:
> /ai-fluency-planning I want to use Claude to refactor a 5K-line Python module. I'll know good output when I see it.

**Expected behaviors** (skill loaded):
- Per the Edge cases rule: pushes once on Discernment with concrete prompts ("what would make this refactor unusable — broken tests? readability regression? new dependencies?").
- If the user still can't articulate, captures the gap explicitly in the brief ("Discernment criteria deferred — apply manual code review and test-suite check until criteria emerge").
- Brief reflects the actual project: D1 likely splits AI-drafts-changes / human-runs-tests / human-owns-merge-decision, D2 prompt template includes "preserve test coverage", "don't introduce new dependencies without flagging".
- File saved as `<name>-AI-Brief.md`.

**Baseline behavior** (skill not loaded):
- Either accepts "I'll know it when I see it" without pushing, or asks an exhaustive list of questions that frustrates the user.

**Pass/fail criterion**: Output pushes on Discernment with at least one concrete prompt, captures the gap if unresolved, and produces a brief with code-project-specific D1 split and D2 prompt template.

---

## Eval 3 — User wants to skip the interview

**Query**:
> /ai-fluency-planning Just give me the template. I'll fill it in myself.

**Expected behaviors** (skill loaded):
- Per Edge cases: honors the user's request. Produces a brief with `[fill in]` placeholders.
- Tells the user which sections most need their attention before the brief becomes useful (typically D2 prompt template and D3 Discernment checklist — the parts that depend on project specifics).
- Saves the placeholder brief to disk.

**Baseline behavior** (skill not loaded):
- Likely refuses to skip, insists on running the interview, or produces an inline template without saving.

**Pass/fail criterion**: Placeholder brief is saved to disk, the user is told which sections are most critical to fill in, and Claude does not insist on running the interview.

---

## Discovery test (trigger eval — see `evals/trigger-eval.json` for the full set)

**Query**: "I'm about to start writing a 30-page market analysis. Can you help me set up how to use Claude for it?"

**Pass**: Claude reads `SKILL.md` and runs the planning interview.
**Fail**: Claude jumps straight to drafting suggestions without invoking the skill — description's "set up before we start" trigger isn't firing.
