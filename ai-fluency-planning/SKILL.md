---
name: ai-fluency-planning
description: >
  Runs a structured pre-execution planning session using the AI Fluency 4D
  Framework (Delegation, Description, Discernment, Diligence) and produces a
  markdown AI Project Brief the user can reference throughout their work. Use
  this skill whenever the user is about to start a project or task and wants to
  set up effective AI collaboration before diving in. Trigger on phrases like:
  "help me plan this with AI", "I want to set up a project", "help me figure
  out how to use Claude for this", "let's plan before we start", "how should I
  approach this task with AI?", "help me write a good prompt for this project",
  "set up an AI brief", or any time the user describes a project they haven't
  started yet and wants structured guidance. Also use this when the user types
  /ai-fluency-planning. Do NOT use for tasks already in progress, simple
  single-step requests, or when the user just wants a quick answer.
---

# /ai-fluency-planning — Pre-Execution Planning

Conduct a focused planning interview, then produce a structured **AI Project Brief** as a markdown file. This brief covers everything the user needs to set up effective, efficient, ethical, and safe AI collaboration — before any real work begins.

This skill applies the 4D Framework in planning mode:
- **Delegation**: What goes to AI vs. human; what mode of interaction
- **Description**: How to communicate — prompt templates for the main tasks
- **Discernment**: What "good" looks like, defined upfront
- **Diligence**: Data sharing, disclosure, and responsibility considerations

## When to use this

- User explicitly types `/ai-fluency-planning`
- User says some variant of "help me plan this with AI", "let's set up before we start", or "help me figure out how to use Claude for this"
- User describes a project they haven't started yet and wants structured guidance
- A multi-step task is about to begin where upfront prompt + scope clarity would compound across iterations

Do NOT trigger for in-progress tasks, simple single-step requests, or quick-answer queries — running the full interview there wastes the user's time.

---

## Step 1 — Interview

Conduct a short, focused interview. Ask questions conversationally — don't dump them all at once. Adapt based on what the user already told you; skip questions they've already answered.

Cover these areas, in roughly this order:

**Project & Goal**
- What is the project or task? What does a successful outcome look like?
- Who is the audience or end user of the output?
- What is the timeline or urgency?

**Delegation**
- Which parts require your own expertise, judgment, or creativity vs. AI assistance?
- What mode fits best: Automation (AI executes instructions), Augmentation (thinking partner back-and-forth), or Agency (AI works semi-independently)?
- Are there any parts you would prefer to keep fully human?

**Description**
- What kind of output(s) do you need? (format, length, style, tone)
- How should AI approach the task? (methods, frameworks, steps, things to avoid)
- How do you want AI to behave during collaboration? (concise vs. detailed, challenge you vs. support you, give options vs. best answer)

**Discernment criteria**
- What would make you confident the AI output is good? (accuracy signals, quality markers, red flags)
- Are there domain-specific things to check — facts, terminology, logic, tone?

**Diligence**
- Will you share any sensitive, confidential, or personal information with AI?
- Who will see the final output, and do they need to know AI was involved?
- What level of verification will the output require before use?

Keep the interview tight. 5–8 focused exchanges is enough for most projects. For simple projects, infer answers and confirm rather than asking from scratch.

---

## Step 2 — Produce the AI Project Brief

Once enough information is gathered, produce the brief. Write it in Markdown. Tell the user what file it is being saved to.

Save to: [workspace folder]/[project-name]-AI-Brief.md

Use this exact structure:

# AI Project Brief — [Project Name]
*Generated [date] using the AI Fluency 4D Framework*

---

## Project Overview

**Goal:** [What this project produces and what success looks like]
**Audience:** [Who will use or see the output]
**Timeline:** [Urgency or deadline]

---

## D1 — Delegation Plan

**Interaction mode:** [Automation / Augmentation / Agency — and why]

| Task / Component | Owner | Rationale |
|-----------------|-------|-----------|
| [Task 1] | Human | [Requires judgment / domain expertise / creativity] |
| [Task 2] | AI | [Synthesis / drafting / pattern recognition] |
| [Task 3] | Both | [Back-and-forth iteration needed] |

**Human-owned decisions:** [List the things only the human should decide]
**AI-assisted areas:** [Where AI adds the most leverage]

---

## D2 — Description Spec

### What AI should produce (Product)
- **Output type:** [document / code / analysis / draft / list / etc.]
- **Format:** [length, structure, headers, sections]
- **Tone & style:** [formal/casual, dense/scannable, assertive/exploratory]
- **Audience calibration:** [reading level, assumed background]

### How AI should approach the task (Process)
[Step-by-step instructions, frameworks to use, reasoning approach, things to avoid]

### How AI should behave (Performance)
- [Concise or thorough?]
- [Challenge or support?]
- [Give options or one best answer?]
- [Ask clarifying questions or make reasonable assumptions?]

### Prompt Template(s)

**Main task prompt:**

[Role/persona if relevant]

Context: [project background, audience, goal]

Task: [specific instruction]

Process: [how to approach it — steps, framework, method]

Output format: [exact format expected — length, structure, sections]

Constraints: [anything to avoid, style rules, word count, etc.]

**Iteration/refinement prompt:**

The output [what was off]. Please revise by [specific change].
Keep [what to preserve]. Focus especially on [priority area].

---

## D3 — Discernment Checklist

*Use this to evaluate AI outputs before accepting them.*

**Product — Is the output good?**
- [ ] [Domain-specific accuracy check]
- [ ] Appropriate tone and style for audience
- [ ] Coherent structure — no internal contradictions
- [ ] Relevant — actually addresses the task, no drift
- [ ] Watch for hallucinations on: [specific high-risk topics for this project]

**Process — Did AI reason well?**
- [ ] Logical flow — conclusions follow from premises
- [ ] Attended to all parts of the request
- [ ] No unsupported leaps in reasoning

**Performance — Did AI behave well?**
- [ ] Responsive to feedback and direction
- [ ] Terminology appropriate for context
- [ ] Communication style served the work

---

## D4 — Diligence Notes

**Data & privacy**
- Information shared with AI: [list anything sensitive or confidential]
- Privacy / IP considerations: [any concerns, or "none identified"]

**Transparency**
- Audience disclosure expectation: [do they need to know AI was involved?]
- How AI contributed: [drafting / research / synthesis / editing / etc.]

**Verification plan**
- What to verify before using output: [specific checks]
- Who is responsible for final accuracy: [the human — always]

**Diligence statement** *(draft — edit before use)*
"In creating this [output], I collaborated with [AI system] to assist with [specific tasks]. All AI-assisted content was reviewed and evaluated. The final output reflects my judgment and I take full responsibility for its accuracy and presentation."

---

## Quick Reference Card

| Phase | Check |
|-------|-------|
| Before each AI interaction | D2 spec — describing product, process, and performance clearly? |
| After each AI output | D3 checklist — product, process, performance all check out? |
| Before sharing | D4 — verified, disclosed appropriately, I can vouch for this? |

---

## Step 3 — Handoff

After saving the brief, tell the user:
1. A link to the file
2. One sentence on which prompt template to start with
3. One specific risk or assumption to watch for in their project

Keep it short. The brief does the heavy lifting. No sycophantic opener, no trailing summary.

---

## Edge cases

**Tasks already in progress**: Skip the brief — assist directly with whatever step they're on. Offer to retro-fit a brief if the work has clearly outgrown its original framing.

**Single-step or quick-answer requests**: Skip the interview. The full 4D pass is overkill for "edit this paragraph" or "what's the syntax for X" — running it would frustrate the user.

**User skips the interview** ("just give me the template"): Honor it. Produce a brief with `[fill in]` placeholders and tell them which sections most need their attention before the brief becomes useful.

**User can't articulate Discernment criteria** ("I'll know it when I see it"): Push once with two or three concrete prompts ("what would make this output unusable for your audience?"), then move on if they still can't answer. Capture the gap in the brief explicitly so they know what's deferred.

**Combined with /deciding (when available)**: A natural sequence — run `/deciding` on whether to undertake the project at all, then run `/ai-fluency-planning` once the choice is settled. If `/deciding` is not in the available skills list, surface this option to the user but proceed with the brief on what they've described.

---

## Reference files

- [`evals/trigger-eval.json`](evals/trigger-eval.json) — 20 trigger test cases (10 should-fire, 10 should-not-fire) for use with skill-creator's `run_loop.py`. Negatives are near-misses: in-progress task help, framework theory questions, model selection, and other planning-adjacent asks that don't warrant the full 4D interview.

## Worked example (excerpt)

**User**: "I want to plan how to use Claude for writing a Q4 board update."

**After 4 short interview exchanges**, the brief opens with:

> # AI Project Brief — Q4 Board Update
> *Generated 2026-05-01 using the AI Fluency 4D Framework*
>
> ## Project Overview
> **Goal:** A 2-page Q4 board update covering revenue, product, headcount, and strategic risks. Success = directors arrive at the meeting with their questions already partly answered.
> **Audience:** Board of directors (5 people, mixed technical fluency).
> **Timeline:** Draft by Friday, send by Monday EOD.
>
> ## D1 — Delegation Plan
> **Interaction mode:** Augmentation — back-and-forth on draft and tone.
>
> | Task | Owner | Rationale |
> |---|---|---|
> | Final narrative + judgment calls | Human | Strategic framing belongs to the CEO |
> | First-draft synthesis from raw bullets | AI | Pattern recognition + prose generation |
> | Numbers and metrics | Human | Source-of-truth must come from the dashboard, not the model |
>
> *(D2 prompt template, D3 checklist, D4 diligence statement follow.)*

**Handoff line**: "Saved to `Q4-board-update-AI-Brief.md`. Start with the Main task prompt in D2. Watch for: AI confidently filling in metric numbers from memory — those are yours to source."
