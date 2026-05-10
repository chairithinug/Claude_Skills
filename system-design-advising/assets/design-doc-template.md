# Design Doc: [System or Feature Name]

**Author(s)**: [names]
**Status**: Draft | In Review | Approved | Implemented
**Last updated**: YYYY-MM-DD
**Reviewers**: [names]

---

## TL;DR

3-5 bullets. The whole document compressed. A reader who only reads this section should know what's being built and why it matters.

## Goals

- What this design *will* deliver
- Measurable where possible

## Non-goals

What this design explicitly will *not* address. Equally important — prevents scope creep and clarifies boundaries.

## Background and context

What's the current state? What problem are we solving? Who's affected? Why now?

Include data — current load, current pain points (with numbers if possible), prior attempts.

## Requirements

### Functional
- What the system must do

### Non-functional (load-bearing pillars)
- Scalability target (RPS, MAU, data volume)
- Latency target (p50, p95, p99)
- Availability target (SLO)
- Security/compliance requirements
- Cost constraints

Name the 2-3 *load-bearing* pillars explicitly.

## Proposed design

### High-level architecture

[Diagram + prose. Diagram alone is decoration; prose alone is hard to follow. Both.]

### Components

For each major component:
- Responsibility
- Interface (API, schema)
- Data ownership
- Failure modes

### Data model

Schema sketches, ownership boundaries, consistency model.

### Request flow

For 1-3 critical paths, walk the flow end-to-end. Include failure handling.

### Deployment

How is this deployed? Rollback strategy? Migration plan if replacing existing system?

### Observability

What logs, metrics, traces? What alerts? What SLIs? Who's on-call?

## Considered alternatives

Two or three alternatives that were genuinely considered. For each:
- What was the alternative
- Why it was rejected (be specific — "complexity" alone isn't a reason)

## Trade-offs

What does this design cost us? Be honest. Every design has costs.

- Operational cost (deploy complexity, on-call burden, observability surface)
- Infrastructure cost (rough monthly $$ at expected load)
- Engineering cost (build time, learning curve)
- Future flexibility cost (what does this lock us into?)

## Anti-patterns avoided

What anti-patterns is this design specifically designed to avoid? (E.g., distributed monolith, premature distribution, no idempotency.)

## Risks and mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| ... | high/med/low | high/med/low | ... |

## Migration plan (if applicable)

Phased rollout, dual-write, shadow traffic, feature flags, rollback criteria.

## Open questions

Honest list of what's not yet decided or not yet known. Doesn't block approval; surfaces what to revisit.

## Timeline (rough)

- Phase 1 (week N): ...
- Phase 2 (week N+M): ...
- Phase 3 (week N+P): ...

## References

- Related ADRs
- External docs / papers
- Prior design docs

---

## Notes on using this template

- Length should match scope. A small change deserves a small doc; a platform overhaul deserves a long one. Both should still have a TL;DR.
- The "Non-goals" section is high-value and underused. Write it.
- "Considered alternatives" with honest reasons protects you from second-guessing later. Future-you forgets why option B was rejected.
- Naming the load-bearing pillars in Requirements forces the rest of the doc to stay honest about trade-offs.
- The Operability sections (Deployment, Observability) are non-optional. Designs without them are incomplete.
