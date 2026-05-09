# Evals — researching-topics

Three representative scenarios that test whether this skill solves the gap it was written for. Run these *without* the skill first to establish baseline, then with the skill installed.

The skill's load-bearing moves are: forced six-step methodology, layered output (TL;DR → key findings with confidence labels → competing views → open questions → sources), and explicit fact-vs-inference labeling. Failure modes: skipping the Frame section, no confidence labels on findings, balancing competing views without steel-manning each, padding with low-quality sources.

---

## Eval 1 — Quick-scan mode (small substantive question)

**Query**:
> /researching-topics quick-scan: what's the current state of GraphRAG adoption in production systems?

**Expected behaviors** (skill loaded):
- States `**Mode**: quick-scan` at the top.
- Output is 300–500 words, single search round.
- TL;DR (3–5 bullets) leads.
- Frame section is brief — one-sentence question restatement + why it matters.
- Key findings each have a confidence label (high / medium / low / inferred).
- Competing views section steel-mans both "GraphRAG is over-hyped at current adoption levels" and "GraphRAG is real and underplayed in agent-RAG conversations".
- Sources cited; load-bearing claims have actual sources, not vibes.
- Closes with a concrete drill-down offer.

**Baseline behavior** (skill not loaded):
- Likely produces a 1500-word essay without TL;DR, no confidence labels, blends own opinion with sourced claims, no competing-views section.

**Pass/fail criterion**: Output declares `Mode: quick-scan`, runs all canonical sections, stays in 300–500 words, has confidence labels on findings.

---

## Eval 2 — Deep-dive mode (genuinely complex topic)

**Query**:
> /researching-topics Build me a view on whether the EU AI Act will materially constrain US-based AI startups deploying in Europe over the next 12 months.

**Expected behaviors** (skill loaded):
- States `**Mode**: deep-dive`.
- Output is 1000+ words.
- Frame restates the question as a forward-looking question (12-month horizon), names the underlying decision (e.g., "should I plan for compliance overhead now").
- Multi-angle search visible in source diversity: regulatory primary sources, industry analyst commentary, contrarian / "the AI Act will under-bite" view, market data on enforcement trajectory.
- Findings labeled with confidence levels and freshness markers ("as of mid-2026", "norms still settling").
- Competing views section is genuine — both "binding constraint" and "paper tiger in practice" cases are steel-manned.
- Open questions explicit; doesn't pretend the question is fully resolved.
- Sources are primary or analyst-grade, not aggregator SEO.

**Baseline behavior** (skill not loaded):
- Likely produces a long summary blending sources without distinguishing facts from inferences. May not steel-man both sides or surface the open questions cleanly.

**Pass/fail criterion**: Output runs the canonical structure, has explicit confidence + freshness labels on findings, steel-mans competing views without flattening to a balanced average, and surfaces ≥ 2 specific open questions.

---

## Eval 3 — Compare-options mode (with consistent criteria)

**Query**:
> /researching-topics compare-options: vLLM vs SGLang vs TensorRT-LLM as inference engines for our 70B model production deployment.

**Expected behaviors** (skill loaded):
- States `**Mode**: compare-options`.
- Comparison criteria stated explicitly before the table (e.g., latency at batch size 1, throughput, hardware support, deployment maturity, KV-cache efficiency, multi-LoRA support).
- Comparison table with consistent rows across all three options.
- Per-option strengths/weaknesses written as comparable bullets, not free-form prose.
- Recommendation: either commits if the criteria favor one option, or names "Option A wins under condition X, Option B under condition Y, Option C under condition Z".
- Open questions section names what user-side data would resolve any remaining gap.
- Sources cited.

**Baseline behavior** (skill not loaded):
- Likely produces a feature-comparison narrative without consistent criteria, often picking inconsistent attributes per option, no conditional recommendation.

**Pass/fail criterion**: Output names criteria explicitly, fills the comparison table consistently across all options, gives a conditional or committed recommendation, and surfaces the user-side data that would tip the call.

---

## Discovery test (trigger eval — see `evals/trigger-eval.json` for the full set)

**Query**: "Look into whether single-cell RNA-seq foundation models are actually production-useful or still research-stage."

**Pass**: Claude reads `SKILL.md` and runs deep-dive mode.
**Fail**: Claude answers with general impressions without invoking the skill — "look into" trigger isn't firing.
