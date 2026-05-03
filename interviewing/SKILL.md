---
name: interviewing
description: >
  Runs a structured interview prep, design, or debrief pass for job interviews —
  from either side of the table. For candidates: decode the role into competencies,
  build a STAR story bank, prep universals (tell-me-about-yourself, why-this-role,
  questions for them), and run a post-interview debrief. For interviewers: design
  a structured interview (job analysis → competencies → behavioral/situational
  questions → behaviorally-anchored rubric) and structure a calibrated panel
  debrief. Includes a cross-cultural layer when relevant. Use when the user types
  /interviewing. Also trigger automatically whenever the user describes a real
  upcoming or recent job interview — as candidate, hiring manager, panel member,
  or recruiter — even casually ("I have a screen Tuesday," "we're hiring an ML
  engineer," "the loop went weirdly today"). Do NOT trigger on theoretical
  questions about hiring, generic "interview tips" with no real context, or
  non-job interviews (journalistic, exit interviews) — answer those directly.
---

# /interviewing — Interview Prep, Design & Debrief

Most job interview outcomes are decided before the interview starts. For the candidate, that means having mapped the role to a story bank, not improvising from memory under stress. For the interviewer, that means having a competency rubric and calibrated questions, not vibing for "culture fit." This skill forces that prep — and runs the post-interview debrief that turns one interview into better performance on the next.

The structural backbone is **competency → behavioral evidence → calibrated judgment**. Both sides of the table use it; they just sit on opposite seats.

## When to use this

- User explicitly types `/interviewing`
- User describes a real interview they are about to enter, are inside, or just finished — as candidate, hiring manager, panel interviewer, or recruiter
- User asks for help with: a story for a behavioral question, designing an interview loop, writing rubric questions, deciding hire/no-hire, debriefing what went well or badly

Do NOT trigger on theoretical/academic questions about hiring science, generic "give me interview tips" with no real situation attached, or non-employment interviews — answer those directly.

## Steps / Workflow

### Step 0 — Pick a mode (state it in one line)

- **interviewee-prep** — candidate preparing for an upcoming interview → load [`references/interviewee-prep.md`](references/interviewee-prep.md)
- **interviewer-design** — designing or preparing to run an interview → load [`references/interviewer-design.md`](references/interviewer-design.md)
- **interview-debrief** — reviewing an interview that already happened (either side) → load [`references/interview-debrief.md`](references/interview-debrief.md)

State the chosen mode at the top of the response. Load **only** the reference file for the chosen mode — that's the whole point of the split. For tactical questions asked while the user is mid-loop ("they just asked me X, what do I say?", "the candidate is rambling, how do I redirect?"), skip the full workflow — see the relevant edge case.

### Step 1 — Run the mode

Each reference file contains a copy-paste checklist and the substantive workflow for its mode. Work through the checklist as you go.

The cross-cultural / remote-format layer lives inside the relevant mode reference (interviewee side in `interviewee-prep.md` step 5; interviewer-panel side in `interviewer-design.md` step 7). Pull it in only when relevant.

## Output format

- Lead with the mode and the diagnosis. No throat-clearing, no recap of the user's situation.
- Use section headers when the situation is complex enough to need them; for a single targeted question, prose is fine. Match length to stakes.
- Every section should reference the user's *specific* situation. Generic advice is a failure mode of this skill.
- For the candidate's STAR stories, write them or co-write them — don't just point at the template. Show what good looks like for this role.
- **Recommend, don't list.** When the user's context clearly favors one option, recommend it and say why. Only present 2–3 options when the trade-offs are genuinely live and depend on user-side information you don't have. Listing options as a way to avoid committing is a soft fail.
- Label inferences as inferences. "Inferred from the JD wording" not "they want you to…".
- End with the single highest-leverage move in the next 24 hours — usually about preparation or specific drilling, not tactics in the room.
- No sycophantic opener, no trailing summary.
- When the user pushes back on a structural recommendation (structured interviews, behavioral evidence, independent scoring before debrief), defend it — these are evidence-backed, not stylistic. When they push back on a convention (thank-you notes, dress code, "what's your weakness" framing), be willing to discuss the trade-off.

## Edge cases

**Mid-interview tactical** — user has a specific tactical question right now, either side. Skip the full workflow; answer fast, then add one line on whether there's a deeper gap worth fixing for *next time*.

- *Candidate side*: "they just asked me X, what do I say?", "I have 30 minutes before the call and they sent me a coding challenge prompt." Give the STAR scaffold applied to the question, or the tactical answer to the challenge framing. Don't run prep mode in 30 minutes.
- *Interviewer side*: "the candidate is rambling, how do I redirect?", "candidate hasn't given me usable evidence on competency X yet." Give the specific verbal move — for redirection, an interrupt-and-pivot script ("That's helpful context — let me jump us forward to the part where you decided to…"); for missing evidence, a more pointed probe ("What specifically did *you* do, separate from what the team did?"). Surface in one line whether the loop's question design is the deeper issue.

**No job description available**: ask once for the role title and 1–2 lines about the team/company. If still nothing, work from competencies common to the role family, flagged as defaults to verify.

**Candidate wants validation, not analysis** ("I think I bombed it, was that really that bad?"): acknowledge first, offer the debrief workflow as an option. Don't run the full thing unsolicited on someone in distress.

**Interview red flags** (interviewer asking illegal questions about marital status / pregnancy / age / national origin in jurisdictions where this is unlawful, hostile interviewer behavior, signs of bait-and-switch on the role): flag plainly, suggest the candidate reconsider whether the offer would even be desirable, and don't optimize purely for getting the offer.

**Hiring panel asks for help selecting between finalists**: this isn't an interview-prep question — it's a decision question. Surface the rubric scores, flag where evidence is thin, and suggest a final calibrated reference check or work sample if the gap is genuinely close.

**Rejected candidate processing the outcome**: support the debrief in Mode C (`references/interview-debrief.md`), explicitly resist post-hoc rationalizing what "really" happened (the candidate usually doesn't have the data). Focus on the next interview, not this one.

**Combined with /negotiating** (when available): A natural sequence — `/interviewing` through the offer, then `/negotiating` on the comp/start-date/scope. Run each cleanly in order; don't blend them. If `/negotiating` is not in the available skills list, complete the interviewing flow and tell the user that structured comp negotiation prep would normally be the next step.

**Combined with /deciding** (when available): When the panel is genuinely split between finalists, or when the candidate is choosing between offers, `/deciding` is the better tool than continuing in interviewing mode. If `/deciding` is not in the available skills list, surface the trade-offs directly and let the user choose.

## Reference files

The three modes are split into separate files so only the relevant mode loads per session. **Read only the file for the mode chosen in Step 0.**

- [`references/interviewee-prep.md`](references/interviewee-prep.md) — Candidate-side prep: decode role → STAR story bank → universals (tell-me-about-yourself, why-this-role, weakness, comp ask, questions for them) → role-specific layer → cross-cultural & remote calibration → failure-mode pre-mortem.
- [`references/interviewer-design.md`](references/interviewer-design.md) — Interviewer-side design: job analysis → behavioral/situational question bank → behaviorally-anchored rubric → loop structure → bias and calibration check → debrief protocol → candidate experience and cross-cultural panel calibration.
- [`references/interview-debrief.md`](references/interview-debrief.md) — Post-interview learning: hygiene (thank-you / score submission) → diagnose specific moments → distinguish performance from process / luck → one thing to do differently → things to actively *not* do.
- [`evals/trigger-eval.json`](evals/trigger-eval.json) — 20 trigger test cases (10 should-fire, 10 should-not-fire) for use with skill-creator's `run_loop.py`. Negatives test the description's explicit exclusions: theoretical hiring questions, generic tips with no situation, non-employment interviews, post-offer comp negotiation, decision-between-finalists.

## Worked example

**User**: "I have a senior PM screen at a fintech Thursday. 45 minutes with the hiring manager. JD emphasizes 0→1 product work and stakeholder alignment. Help me prep."

**Output (interviewee-prep mode)**:

> **Mode**: interviewee-prep
>
> **Diagnosis**: 0→1 + stakeholder alignment in fintech is a tight competency profile — the screen will likely test (a) ambiguity tolerance, (b) execution under fragmented stakeholders, (c) how you make decisions without complete data. Compliance/regulatory awareness is a likely supporting probe given fintech.
>
> **Story bank gap-check**: from your background, you have one strong 0→1 story (the marketplace launch) and one strong stakeholder-alignment story (the cross-team rollout). You're light on the "decision under ambiguity" angle — that's the gap to close before Thursday.
>
> **Universals to draft tonight**:
> - *Why fintech, why this company*: needs to reference something specific in their public roadmap, not "I love your mission."
> - *Tell me about yourself*: 90 seconds, ending with what about *this specific role* fits the trajectory — not your whole career.
>
> **Role-specific drill**: practice articulating a product trade-off out loud, with someone watching, in 5 minutes. The performance gap between silent and observed practice is large.
>
> **Highest-leverage move in next 24 hours**: write the "decision under ambiguity" story tonight. It's your gap. Use STAR; aim for ~50% on the Action portion.
>
> If useful, I can co-draft that ambiguity story now, or pressure-test your "tell me about yourself" arc.

(Worked examples for interviewer-design and interview-debrief modes follow the same shape — lead with mode + diagnosis, identify the gap, name the highest-leverage move.)
