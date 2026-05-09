# Evals — ai-solution-advising

Three representative scenarios that test whether this skill solves the gap it was written for. Run these *without* the skill first to establish baseline, then with the skill installed.

Scenarios stress different modes from the Mode Routing table so we know the skill isn't only good at one slice.

---

## Eval 1 — Solution-Design (the "build vs. don't-build" call)

**Query**:
> We're a mid-size B2B SaaS. Customer support tickets are growing 30% MoM. CTO wants to build an agentic AI to handle Tier-1 tickets autonomously. Where should we start?

**Expected behaviors** (skill loaded):
- Frames the actual business outcome (deflection × resolution quality at constant or declining cost-per-ticket), not the architecture.
- Pushes back on "agentic" as the right starting pattern. Recommends a workflow (classify → retrieve → draft → escalate-or-send) before any agent.
- Names the concrete stack with parameters: classifier (Haiku or fine-tuned small model + 300–500 labeled tickets), hybrid retrieval + reranker, structured-output drafter, guardrails, HITL.
- Names at least 3 failure modes specific to this approach (bad retrieval, hallucinated features, confidence collapse, agentic loop cost runaway).
- Defines a concrete eval bundle: Recall@5, classifier F1, deflection rate, CSAT delta, cost-per-ticket alert threshold.
- Provides a path-to-production with timeline and decision criteria (POC weeks, shadow mode, canary).
- Reversibility check is explicit (workflow → agentic upgrade is cheap; agentic-first → workflow rollback is expensive).

**Baseline behavior** (skill not loaded):
- Likely says "yes, build the agent" or describes a generic agentic architecture from a vendor pitch. Misses the workflow-first move. Doesn't quantify eval. Probably skips the reversibility framing.

**Pass/fail criterion**: Output explicitly recommends a workflow over an agent for the first build, names ≥3 failure modes, gives a concrete eval bundle with numeric thresholds, and includes a reversibility / rollback consideration.

---

## Eval 2 — Engineering Deep-Dive (the "this implementation choice" call)

**Query**:
> We're building Q&A over a 50K-document corpus. Tried naive RAG, getting 60% answer accuracy. Boss wants to throw GraphRAG at it. Should we?

**Expected behaviors** (skill loaded):
- Refuses to recommend GraphRAG without diagnosing the *current* failure: is it retrieval recall, retrieval precision, drafting/grounding, or eval-set quality?
- Recommends advanced-RAG upgrades first: hybrid retrieval (BM25 + dense), reranker, contextual retrieval, chunking-strategy review. Names parameters (top_k, reranker model, chunk size).
- Names when GraphRAG actually pays off (entity-rich corpora, multi-hop questions where the answer requires connecting concepts across documents). Names when it doesn't (factual lookup, single-source answers).
- Surfaces "Don't Add That" framing: GraphRAG adds significant complexity (graph construction, graph maintenance, query rewriting) that should be earned with measurement, not assumed.
- Requires an eval set: accuracy on what eval? per category? Without a stratified eval, every architecture decision is theatrical.
- Names the diagnostic procedure: build a labeled eval set of ~200 Q&A pairs stratified by question type, measure retrieval Recall@k and answer faithfulness separately, then choose the upgrade matched to the failure mode.

**Baseline behavior** (skill not loaded):
- Likely explains GraphRAG and recommends building it. Misses the diagnostic step, the "patterns endure, tools change" framing, and the eval-first approach.

**Pass/fail criterion**: Output requires a diagnostic before recommending any architecture upgrade, names ≥2 advanced-RAG moves cheaper than GraphRAG, explicitly distinguishes when GraphRAG pays off vs. not, and demands an eval set with stratification.

---

## Eval 3 — Governance + Knowledge-Currency (the "is what we know still right" call)

**Query**:
> We're a healthcare SaaS deploying an LLM for clinical-note summarization to physicians in the EU. CEO is asking about EU AI Act compliance. What do we need to know?

**Expected behaviors** (skill loaded):
- Reads `references/knowledge-version.md` and surfaces staleness if applicable (the EU AI Act enforcement timeline is still evolving — flag if the skill's last refresh predates a known enforcement milestone).
- Frames the regulatory regime: EU AI Act is risk-classified; clinical decision-support assisting medical professionals is likely high-risk under Annex III. Map to controls: data governance, technical documentation, human oversight, accuracy / robustness / cybersecurity, post-market monitoring.
- Names overlap and divergence with NIST AI RMF (US) and any sovereign-AI considerations if the deployment is hosted outside the EU.
- Surfaces what's negotiable (deployment topology, evaluation cadence, vendor selection) vs. what's not (high-risk classification once it lands; CE marking and conformity assessment are regulatory, not negotiable).
- Names the human-in-the-loop pattern as load-bearing for this use case: physician must remain the decision-maker; the LLM produces a draft summary; the audit trail must be defensible.
- Recommends concrete operating-model moves: appoint an EU representative if the provider isn't EU-based; establish a quality management system aligned to ISO/IEC 42001 (when applicable) or equivalent.
- Is explicit about its own currency limit: "Verify the latest enforcement guidance before committing — search the EU AI Office's published guidance for [specific regime question]."

**Baseline behavior** (skill not loaded):
- Likely produces a generic "EU AI Act compliance checklist" copy-pasted from public summaries. May confuse risk classes. Unlikely to surface NIST-comparison or sovereign-AI considerations. Probably doesn't surface its own knowledge cutoff.

**Pass/fail criterion**: Output classifies the use case under the AI Act risk framework, names the top-5 control areas required for high-risk systems, distinguishes negotiable from non-negotiable controls, references HITL as load-bearing, and explicitly flags currency limits with a search recommendation.

---

## Discovery test (trigger eval — see `evals/trigger-eval.json` for the full set)

Before measuring output quality, confirm the skill triggers at all on a natural-language query:

**Query**: "We're trying to figure out whether to fine-tune Llama or just stay with Claude + RAG for our use case. Thoughts?"

**Pass**: Claude reads `SKILL.md` (visible in tool calls).
**Fail**: Claude answers without loading the skill → the description is broken; iterate on it before iterating on the body.
