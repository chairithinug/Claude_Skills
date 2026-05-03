---
name: researching-topics
description: >
  Conducts substantive topic research using a forced six-step methodology
  (frame → map → plan sources → execute → synthesize → verify) and produces
  layered output: TL;DR → key findings with confidence levels → competing
  views → open questions → sources. Use whenever the user types
  /researching-topics, or asks to research, investigate, look into, dig into,
  build a view on, or do a deep dive on a topic. Trigger on phrases like
  "research X", "look into X", "investigate X", "deep dive on X", "build a
  view on X", "what's the story with X", "compare X vs Y vs Z", "should I
  [decision based on topic]". Three modes: quick-scan (~5–10 min depth,
  300–500 words), deep-dive (default, multi-step, ~1000+ words),
  compare-options (consistent criteria across alternatives). Do NOT use for
  simple fact lookups ("what year did X happen", "who is the CEO of Y"),
  how-to or procedural questions, code questions, or single-claim
  verification — those don't need the methodology overhead.
---

# /researching-topics — Forced Methodology for Topic Research

Forced methodology for substantive topic research. The value here is **structure**, not the act of searching — Claude already searches well. This skill enforces explicit framing, multi-angle source planning, fact-vs-inference labeling, and consistent layered output.

If a request is a fact lookup, how-to, or single-claim verification, **do not run this methodology** — answer directly. The methodology earns its keep on substantive research, not on every query that mentions a topic.

## When to use this

- User explicitly types `/researching-topics`
- User asks to research / investigate / look into / dig into / build a view on / deep-dive on a topic
- User asks "what's the story with X", "compare X vs Y vs Z", or "should I [decision dependent on topic]"
- A multi-source, multi-angle question is on the table that benefits from explicit framing and confidence labeling

Do NOT trigger for fact lookups, how-to/procedural questions, code questions, or single-claim verification — answer those directly.

---

## Step 1 — Pick a mode (state it in one line)

- **quick-scan** — ≤10 minutes equivalent depth, ~300–500 words. Single search round, light source planning.
  - *Cues:* "quick", "fast take", "TL;DR style", short questions, low-stakes decisions
- **deep-dive** *(default)* — Multi-step, full methodology, ~1000+ words. Multiple search rounds, `web_fetch` on load-bearing sources.
  - *Cues:* default if no other mode signals; substantive decision support; user asks for thorough analysis
- **compare-options** — Consistent criteria across N named alternatives.
  - *Cues:* "compare", "vs.", multiple named alternatives, "which should I pick"

State the chosen mode in the output (`**Mode**: deep-dive`).

---

## Step 2 — Frame

Before searching:
- Restate the question in one sentence
- Identify the underlying decision or question being supported (why does this matter?)
- Define what would actually resolve it — what evidence would change the answer?

**Prefer a stated assumption over a clarifying question.** Asking costs the user a turn; stating an interpretation lets them correct it cheaply if needed. Only ask if proceeding without clarification would clearly waste effort.

The Frame appears in the output as a brief section after the TL;DR — making the assumption explicit lets the user calibrate trust and request a re-aim if they wanted something different.

---

## Step 3 — Map (internal)

- List what's already known or assumed (briefly — don't pad)
- Surface key unknowns: what would a good answer need to fill in?
- **Distinguish well-established knowledge from dynamic claims.** Foundational material (e.g., Belmont Report principles, Popper's falsification, IMRaD structure, FAIR principles) is settled and rarely needs searching — citing it as common knowledge is fine. Current state of debates, recent statistics, adoption rates, and developments since the knowledge cutoff need search and citation.

This step is internal planning — it does not appear in the output. Its job is to focus the source plan and prevent wasted searches on settled material.

---

## Step 4 — Plan sources (internal)

Choose source *types* before running queries:
- **Primary documents** — filings, papers, official statements, regulatory data
- **Expert commentary** — recognized analysts, peer-reviewed work
- **Market / news** — current state, recent developments
- **Contrarian / skeptical** — steel-man the opposing view

Plan internally; the source plan does not appear as a separate output section. The sources actually used appear in the final Sources section.

---

## Step 5 — Execute

- Run multi-angle queries — at minimum 2–3 distinct framings for deep-dive
- Use `web_fetch` for any source that's load-bearing for a finding (don't rely on snippets alone)
- Avoid SEO-bait aggregators when primary sources are accessible
- For non-English-dominant domains (foreign-market equities, regional regulatory texts, country-specific cultural questions, vernacular technical communities), search in the relevant language too

---

## Step 6 — Synthesize (the output)

### Default structure (quick-scan and deep-dive)

```
**Mode**: [quick-scan / deep-dive]

**TL;DR**
- [3–5 bullets. The actual answer. Not a summary of what's coming.]

**Frame** *(include when the topic admits multiple readings, or a non-obvious scoping choice was made)*
- [One short paragraph stating the interpretation/scope. Offer to re-aim if wrong.]

**Key findings**
- [Finding 1] *(confidence: high / medium / low — brief justification, especially when low or contested)*
- [Finding 2] *(confidence: ...)*
...

**Competing views / disagreements**
- [Position A and its strongest case]
- [Position B and its strongest case]

**Open questions / unknowns**
- [What's not resolved by available evidence]

**Sources**
- [Cited sources for load-bearing findings]

[Closing: short, specific drill-down offer — "If useful, I can go deeper into [angle 1], [angle 2], or [angle tied to user's context]." Be concrete; generic "let me know if you want more" is throat-clearing. Skip if the topic is genuinely exhausted.]
```

For time-sensitive claims, add a brief freshness marker inline (e.g., "as of mid-2026", "norms still settling", "current as of [date]") rather than a separate section. The reader should be able to tell at a glance which claims have a shelf life.

### compare-options structure

```
**Mode**: compare-options

**TL;DR**
- [3–5 bullets. The recommendation if criteria favor one option, or the key trade-offs.]

**Comparison criteria**: [list the criteria used]

| Criterion | Option A | Option B | Option C |
|---|---|---|---|
...

**Per-option strengths / weaknesses**
- Option A: [strengths] / [weaknesses]
- Option B: ...
- Option C: ...

**Recommendation**: [if criteria favor one, state it; otherwise state under what conditions each wins]

**Open questions / unknowns**
- ...

**Sources**
- ...
```

---

## Step 7 — Verify (before finalizing)

Self-check pass:
- Are load-bearing claims actually supported by cited sources?
- Is fact distinguished from inference? Inference should be labeled ("this suggests", "likely", "inferred").
- Hedging on settled facts? Don't.
- Stating contested claims as settled? Don't.
- Were competing views steel-manned, or strawmanned?
- Did the chosen mode actually fit the depth of the answer?
- Are time-sensitive claims marked with their currency?

If a load-bearing claim isn't well-supported, downgrade its confidence or remove it.

---

## Cross-cutting: use available context

If user memories, preferences, or prior turns in the same conversation provide relevant context (background, expertise level, current projects, decisions in flight), use it to:
- Calibrate technical depth — don't over-explain familiar territory
- Pick examples that connect to the user's domain
- Highlight angles most relevant to their work or stated goals

For **serial research within the same conversation** (the user asks several related research questions in a row), connect new findings to threads from prior turns ("covered in the previous turn", "extending what was discussed about X") and don't repeat material already covered. Maintain a consistent output structure across turns so the user can navigate the series easily.

**Do not over-personalize.** The research itself stays substantive and even-handed; context shapes emphasis, examples, and the closing drill-down offer — not the underlying analysis or the confidence levels.

---

## Tone & behavior

- Lead with the answer. TL;DR is the answer, not throat-clearing.
- Calibrate confidence: don't hedge settled facts; label genuinely uncertain claims.
- Default to stating an assumption rather than asking a clarifying question. One question max, only when proceeding would clearly waste effort.
- Don't pad. Match length to mode.
- Inference is fine — just label it.
- Steel-man competing views with their strongest case — never strawman.
- No sycophantic openers ("Great question!"), no trailing summaries. The closing drill-down offer is allowed and useful when concrete.

---

## When NOT to use this skill

- Simple fact lookup: "what year did X happen", "who is CEO of Y" — just answer
- How-to / procedural: "how do I do X" — answer directly
- Code questions — answer directly
- Single-claim verification: "is this true: [claim]" — verify, don't run methodology
- The user asks for an opinion or take, not research

---

## Edge cases

- **Topic too broad**: State the interpretation in the Frame section, proceed at that interpretation, and offer to re-aim. Don't ask first — asking costs the user a turn.
- **Sparse sources**: If a reasonable search yields weak sources, say so under "Open questions" rather than padding with low-quality citations.
- **Fast-changing topic**: Mark time-sensitive claims inline ("as of [date]", "norms still settling", "rapidly evolving"). Don't bury time-sensitivity in a separate section.
- **Conflicting sources**: Don't average them — surface the conflict explicitly under "Competing views" with each side's strongest case.
- **Non-English context**: For region-specific or vernacular topics, search in the relevant language and cite the original source.
- **Serial research in same conversation**: Reference prior turns explicitly and build on them rather than repeating. Maintain a consistent output structure across the series so the user can navigate it. Adjust the Frame section to flag the connection ("extending the methodology discussion above into the practical 'how' layer").
- **Combined with /deciding** (when available): A natural sequence — research a topic to inform a decision, then run `/deciding` on the choice itself. If `/deciding` is not in the available skills list, complete the research and note that a decision-framework pass would be the natural follow-up.

---

## Worked example (excerpt)

**User**: "Research whether GraphQL is still worth adopting in 2026 for new projects."

**After running the methodology**:

> **Mode**: deep-dive
>
> **TL;DR**
> - GraphQL retains specific wins (over-fetching reduction, single endpoint for federated UIs, mature tooling) but its momentum has cooled — fewer new framework launches, more "REST + tRPC is enough" discussions *(medium confidence on adoption-trend direction)*
> - For greenfield apps serving heterogeneous clients (web + mobile + partner API), GraphQL still wins on payload efficiency and schema reuse *(high confidence)*
> - For internal services and small teams, tRPC and OpenAPI 3.x have closed the productivity gap; GraphQL's overhead may not pay back *(high confidence)*
>
> **Frame**
> - Reading "worth adopting" as a fresh-build decision, not migrating an existing REST API. Re-aim if migration-cost analysis is what's wanted.
>
> **Key findings**
> - HTTP-caching story still rougher than REST: standard cache layers don't apply natively, requiring resolver-level cache or CDN-aware schemas *(high confidence)*
> - N+1 query problem requires DataLoader discipline; teams without it report worse latency than REST equivalents *(high confidence)*
> - Strong fit when the same backend serves heterogeneous clients — a single schema beats versioned REST *(high confidence)*
>
> **Competing views**
> - Pro-GraphQL: federation has matured, frontend dev velocity wins are real, schema-first design enforces contracts the REST world doesn't.
> - Pro-REST: HTTP semantics are free, caching/auth/rate-limiting tooling is decades-deep, and tRPC + Zod give typed contracts without the GraphQL learning curve.
>
> **Open questions**
> - Whether the client topology actually has the heterogeneity GraphQL solves for
> - Whether the team has operational maturity for resolver-level caching and N+1 discipline
>
> **Sources**
> - [Public benchmark posts, ADRs from open-source projects, framework community discussions]
>
> If useful, I can drill into the federation maturity question specifically, compare GraphQL vs tRPC for small-team contexts, or run the migration-cost view.

The TL;DR is the answer. Everything else supports it. The Frame makes the scoping choice visible. The closing offer is concrete, not generic.
