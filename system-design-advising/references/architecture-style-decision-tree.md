# Architecture Style Decision Tree

## The 2026 default heuristic

**Start with a modular monolith.** Single deployable unit with clean internal module boundaries. This is the right answer for most teams in most situations. Extract services *only* when you have a specific reason — not because microservices are fashionable.

The 2025-2026 industry shift: ~42% of organizations that adopted microservices have consolidated services back into larger deployable units. The driver is cost and operational overhead, not technical limitations.

## The decision tree

Walk these in order. First "yes" wins.

### 1. Are you a team of <10 engineers?
→ **Modular monolith** is almost always right. Microservices benefits only appear at >10 engineers. Below that, you pay all the distributed-systems costs and gain nothing.

Exception: if the team is split into sub-teams by deployment cadence (mobile, backend, data) and they truly cannot share a deploy pipeline, services may help.

### 2. Are you pre-product-market-fit or pre-scale (<100k MAU, <1k RPS)?
→ **Modular monolith.** Optimize for change velocity and learning, not future scale. You will rewrite this; don't pre-optimize for problems you don't have.

### 3. Do you have a genuine need for independent scaling?
"Genuine" means: one component (payment service, ML inference, video transcoding) requires 10×+ the compute of the rest, AND its load profile differs (bursty vs. steady, heavy vs. light).

→ Yes → consider extracting *just that component* as a service. Keep the rest in the monolith.
→ No → modular monolith.

### 4. Do you have polyglot requirements?
"Polyglot" means: one part requires a fundamentally different runtime (ML in Python, core in Java, real-time in Go) and unifying isn't realistic.

→ Yes → extract along language boundaries.
→ No → modular monolith.

### 5. Do you have regulatory isolation requirements?
PCI DSS for payment processing, HIPAA for PHI handling, SOX for financial reporting. These often *require* physical separation of code/data.

→ Yes → extract along regulatory boundaries.
→ No → continue.

### 6. Are you >50-100 engineers with Conway's Law pressure?
At this size, organizational structure forces architectural boundaries whether you want them or not. Independent deploy cadences become necessary for team velocity.

→ Yes → microservices, but disciplined: 1 service per team, not 1 service per feature. Service boundaries follow team boundaries.
→ No → modular monolith with selective extraction.

### 7. Is the workload truly bursty / event-driven with idle periods?
Image processing, batch jobs, occasional webhooks, scheduled tasks.

→ Yes → consider serverless (Lambda / Cloud Run / Cloud Functions) for *those workloads*. Not the whole system.
→ No → continue.

### 8. Is the system fundamentally about events / state changes?
Order processing, IoT telemetry, audit pipelines, real-time analytics.

→ Yes → consider event-driven architecture (Kafka, event sourcing, CQRS) for the relevant slice.
→ No → request/response is fine.

## The styles

### Monolith (single deployable, tightly coupled)
- Pros: simplest, fastest deploys, easy debug, no distributed-systems debt
- Cons: scaling ceiling, deploy risk grows with codebase, team coordination cost at scale
- Right for: solo / very small team / early product

### Modular monolith (single deployable, internally modular)
- Pros: simplicity of monolith + modularity benefits, evolutionary path to services
- Cons: requires module-boundary discipline, single-process scaling ceiling
- Right for: most small-to-medium teams, most early-to-mid-stage products
- Example success: GitHub (Rails monolith serving millions), Shopify (modular monolith with selective service extraction), Basecamp

### Microservices (many independent deployables)
- Pros: independent scaling, polyglot, team autonomy, regulatory isolation
- Cons: 3-6× infrastructure cost, distributed-systems debugging, requires platform team, observability burden
- Right for: large teams (>50-100 engineers), genuine independent-scaling needs, regulatory/polyglot requirements
- Example success: Netflix (1000+ services), Uber (thousands of services across regions)
- Common failure mode: distributed monolith (services that can't be deployed independently)

### Serverless / FaaS
- Pros: zero idle cost, auto-scaling, no server management
- Cons: cold starts, vendor lock-in, debugging harder, unsuitable for steady high load
- Right for: bursty workloads, event handlers, glue code, occasional jobs

### Event-driven architecture
- Pros: loose coupling, natural async, audit trail, replay-ability
- Cons: eventual consistency complexity, harder to reason about end-to-end flows, requires schema discipline
- Right for: domains with state changes as the core abstraction (commerce, IoT, analytics)

## Anti-decisions

Direct callouts to make in consultations:

- **"Microservices because everyone does"** — name it. Conway's Law isn't optional but cargo-culting is.
- **"We'll start with microservices to avoid migration later"** — false economy. The migration cost is dwarfed by the running cost of distributed systems you don't need yet.
- **"Monolith because microservices are too hard"** — also wrong if the team is genuinely 50+ engineers fighting over deploys.
- **"Serverless for everything"** — vendor lock-in + cold starts + per-request cost. Not a default.

## What to ask when this comes up

1. How many engineers will work on this in 12 months?
2. What's the current and projected load (RPS, users, data)?
3. Are there any components with fundamentally different scaling profiles?
4. Are there regulatory or language constraints?
5. What's your DevOps maturity (platform engineers, on-call, CI/CD)?

If the answers point to "small team, modest scale, no special requirements" — recommend modular monolith and don't apologize for it.
