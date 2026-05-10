# Layered Analysis — The 6-Pillar Framework

## Why this exists

Every architecture trades off the same six concerns. There is no Pareto-dominant design. The job is to identify which 2-3 are *load-bearing* for the user's situation and optimize for those, accepting trade-offs on the rest.

Naming the load-bearing pillars upfront forces honesty. A team that says "we want maximum scalability AND simplicity AND cost-efficiency" is going to be disappointed; you can have any two strongly, not all three.

## The pillars

### 1. Scalability

Can it handle more load? Two distinct types:
- **Vertical** (bigger machine) — simple, capped by hardware, single point of failure
- **Horizontal** (more machines) — modern default; requires statelessness and harder coordination

Stateless services scale horizontally cheaply. Stateful ones force sharding/replication problems. Recognize which parts of the system are stateful (databases, sessions, in-memory caches) — they're the bottleneck.

### 2. Reliability / availability

Reliability = correctness under failure. Availability = uptime percentage. They're different.
- 99% = 3.65 days down/year
- 99.9% = 8.76 hours
- 99.99% = 52 minutes
- 99.999% = 5.26 minutes

Each nine roughly 10× the engineering cost. Don't promise nines you can't pay for.

Failures are inevitable. Design *for* them, don't try to *prevent* them.

### 3. Performance

Latency (per-request time) and throughput (requests per second). They're different and can trade off.
- Optimizing tail latency (p99, p999) often requires sacrificing throughput.
- Batching improves throughput but hurts latency.
- Caching improves both at the cost of staleness.

Always specify which percentile matters. "Fast" without a percentile is meaningless.

### 4. Maintainability

Can the next engineer reason about and change this without dread? Often dominates total cost of ownership over a system's lifetime. Boring, well-documented, conventional choices win.

Signal of poor maintainability: new engineers take months to ship their first meaningful change.

### 5. Cost

Explicit constraint in 2026, not afterthought. Includes:
- Infrastructure (compute, storage, network egress)
- Platform engineering (people who keep the system running)
- Operational overhead (on-call burden, incident response)
- Opportunity cost (engineering time spent on infra vs. product)

Microservices infrastructure costs ~3.75-6× equivalent monolith functionality. Personnel costs add another layer — platform engineers are expensive and required at scale.

### 6. Security

Now usually counted as the sixth pillar. Designed in from day one is cheaper than patched later.
- Zero-trust networking (TLS internal too)
- Defense in depth
- Principle of least privilege
- Auth at edge + at service boundaries
- Audit logging

## How to apply this in a consultation

For greenfield: walk all six. Force the user to name 2-3 as load-bearing.

For review: identify which the existing design optimized for, which it sacrificed. Surface mismatches between intent and reality.

For scale-diagnose: lead with the pillar the symptom points to (slow = performance; outages = reliability; bills exploding = cost).

For decision-support: name how each option scores on each pillar. Decisions usually become obvious once the load-bearing pillars are named.

## Common mismatches

- Optimizing maintainability claims while shipping microservices for a 5-engineer team
- Optimizing scalability claims while running on a single Postgres instance
- Optimizing cost claims while running 24/7 idle Kubernetes clusters
- Optimizing reliability claims with no observability stack
- Optimizing security claims without TLS internal or audit logs

When you see a mismatch, name it directly.
