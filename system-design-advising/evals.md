# Evals — system-design-advising

Three representative scenarios that test whether this skill solves the gap it was written for. Run these *without* the skill first to establish baseline, then with the skill installed.

The skill's load-bearing moves: **mode routing** (quick / greenfield / review / scale-diagnose / decision-support), **constraint elicitation before prescription**, **explicit trade-offs and operability bar on every recommendation**. Failure modes the skill explicitly resists: canned best-practice dumps, ivory-tower architecture, recommending fixes blind in scale-diagnose, throwing diagrams at strategic-decision questions.

---

## Eval 1 — Greenfield (foundational architecture, partial context)

**Query**:
> /system-design-advising We're building a B2B SaaS for healthcare claim adjudication. Solo founder, planning to hire 2 engineers in 6 months. Need to handle PHI. What architecture should we start with?

**Expected behaviors** (skill loaded):
- Picks `greenfield` mode and states it.
- Elicits the missing-and-load-bearing constraints: scale projection, latency/consistency targets, multi-region need, cost ceiling, foundational-vs-reversible scope. Caps at 2 questions per the workflow.
- States safe assumptions explicitly (single region, cost-sensitive, common cloud) and invites correction.
- Does NOT skip to a recommendation without naming the load-bearing constraint (PHI / HIPAA, solo→small-team trajectory, regulated domain).
- Layered analysis touches the layers that matter — security/compliance first (HIPAA pushes architecture), data layer (audit-log retention, encryption at rest, PHI segregation), architecture style (modular monolith default given team size), API style.
- Recommendation is a **modular monolith** with a one-line trade-off ("buys deployment simplicity and team-friendly debugging; costs less independent scaling") plus flip conditions.
- Anti-patterns flagged: premature microservices, treating compliance as a post-hoc layer, choosing managed services without verifying their HIPAA BAAs.
- Operability bar is concrete: deployment (CI/CD, rollback), observability (PHI redaction in logs is load-bearing), on-call (solo founder = real risk), monthly cost anchor.

**Baseline behavior** (skill not loaded):
- Likely produces a generic "modern SaaS architecture" pitch with microservices, Kubernetes, multi-region, observability stack — overshooting team scale by an order of magnitude. Misses HIPAA-specific data-layer concerns. No operability cost named.

**Pass/fail criterion**: Output names mode, asks ≤2 elicitation questions OR states safe assumptions, recommends modular monolith with trade-off + flip condition, surfaces HIPAA-specific data-layer requirements, names operability bar (deployment, observability, on-call, monthly cost anchor).

---

## Eval 2 — Scale-diagnose (don't recommend fixes blind)

**Query**:
> /system-design-advising Our Postgres is hitting 80% CPU at peak. Boss wants to shard. Worth it?

**Expected behaviors** (skill loaded):
- Picks `scale-diagnose` mode and states it.
- Diagnosis names that 80% CPU is a symptom signal but does not by itself indicate a row-volume problem (which sharding fixes) vs. hot-row contention vs. index-design issues vs. connection-pool problems.
- Recommends what to **measure first** before recommending any fix: top-N slow queries by total time × frequency, index-hit ratio, connection-count vs. `max_connections`, per-table write rate, hot-row distribution.
- Likely-fixes ranked by ROI: index audit + slow-query rewrites first (cheapest), then read replicas (if read-heavy), connection pooling (if connections are the bottleneck), vertical scale (buys time), sharding LAST.
- Names the flip condition that would make sharding the right answer (single multi-TB table, even write distribution, already at max single-primary capacity).
- Confidence is high on diagnosis-first, medium on the specific ranked fixes (because ranking depends on measurement).

**Baseline behavior** (skill not loaded):
- Likely says "yes, shard" or "consider sharding, but also caching, read replicas, query optimization" — a list without a measurement-first frame.

**Pass/fail criterion**: Output explicitly resists recommending sharding without measurement, names what to measure first, ranks alternative fixes by ROI with sharding LAST, states the flip condition that would justify sharding.

---

## Eval 3 — Quick mode (don't burn the user's time on a 2-paragraph question)

**Query**:
> /system-design-advising quick: REST or gRPC for an internal service-to-service API in a 5-person team?

**Expected behaviors** (skill loaded):
- Picks `quick` mode and states it.
- Output is ≤300 words.
- One-paragraph diagnosis-and-recommendation: REST is the default (lower friction, every tool supports it, debuggable from a browser); gRPC pays off when you need streaming, low-latency tight protobuf contracts across many services, or polyglot performance-sensitive pieces.
- One-line flip condition (e.g., "if you have >10 services and shared protobuf contracts already, gRPC's contracts pay off; otherwise REST + OpenAPI is the lower-friction call").
- Optional drill-down offer if the user wants depth.
- Does NOT run the full 7-step methodology. Does NOT produce a 2000-word essay.

**Baseline behavior** (skill not loaded):
- Likely produces a long comparison table of REST vs gRPC features without naming the team's actual context as the deciding factor.

**Pass/fail criterion**: Output is ≤300 words, declares quick mode, recommends with trade-off in same paragraph, states a flip condition, ends with optional drill-down.

---

## Discovery test (trigger eval — see `evals/trigger-eval.json` for the full set)

**Query**: "Database is the bottleneck on our peak traffic days. Where do I look first?"

**Pass**: Claude reads `SKILL.md` and runs scale-diagnose mode.
**Fail**: Claude treats it as a generic Q&A and lists "things to check" without invoking the skill — auto-trigger on real-system-pain signals isn't firing.
