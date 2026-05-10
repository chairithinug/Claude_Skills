# Anti-Pattern Library

Common architectural anti-patterns. Each entry has: how to spot it, why it's bad, what to do instead.

## Distributed monolith

**Spot it**: services that look split but must be deployed together; shared database across "separate" services; can't change one without coordinating with others.

**Why bad**: pays all of microservices' costs (network latency, deployment complexity, observability burden, infrastructure cost) without any of the benefits (independent deployment, isolation, autonomy).

**Instead**: either truly decouple (separate databases, async communication, versioned APIs) or re-merge into a modular monolith. Half-decoupled is the worst place to be.

## Ivory Tower Architect

**Spot it**: architecture documents that don't mention deployment, monitoring, on-call burden, or cost. Diagrams that show clean boxes and arrows but no error paths. Architects who don't write code or take pager rotations.

**Why bad**: produces designs that look right on paper but can't be operated. The team building it absorbs the operational cost the architect didn't reason about.

**Instead**: architects must own at least one operational responsibility (on-call, code review, hands-on prototyping). Every design must answer the operability questions: how is this deployed, how do we know it's broken, who's on-call, what does it cost?

## Premature distribution

**Spot it**: 5-engineer team with 12 microservices. "We're going to need to scale" as the justification before any scale exists.

**Why bad**: pays distribution cost (3-6× infrastructure, platform engineering, observability) before any scale benefit. Team velocity drops because every change requires multi-service coordination.

**Instead**: modular monolith first. Extract services only when you have a specific reason (independent scaling need, polyglot requirement, regulatory boundary, team-size pressure).

## Database as integration bus

**Spot it**: multiple services reading/writing the same database tables. Schema changes break consumers nobody knew about. Application logic embedded in database triggers.

**Why bad**: tight coupling through schema. Changes ripple unpredictably. No clear ownership. No API contract.

**Instead**: services own their data; communication happens through APIs (sync) or events (async). If services need to share data, replicate it explicitly with clear ownership of the source of truth.

## Two-phase commit at scale

**Spot it**: distributed transactions with XA, 2PC, or "we use Spring transactions across services."

**Why bad**: doesn't scale. Locks held across network boundaries. Coordinator failure is catastrophic. Works in textbooks; fails in production.

**Instead**: saga pattern (sequence of local transactions with compensating actions). Often: redesign the workflow so distributed transactions aren't needed.

## Sync chains

**Spot it**: A calls B calls C calls D calls E, all synchronously, all blocking. End-to-end latency is the sum of all hops.

**Why bad**: tail latency multiplies. p99 of the chain ≈ p99 of the slowest hop, but availability multiplies down (each 99.9% service in a chain of 5 = 99.5% combined). One slow downstream slows everything.

**Instead**: async where possible (events, queues). Edge composition (BFF aggregates parallel calls). Service consolidation if the chain reflects unnecessary boundaries.

## Microservices because everyone does

**Spot it**: "We're going to use microservices" as a starting position. No specific architectural problem named that microservices solve. The justification is "best practice" or "what FAANG does."

**Why bad**: cargo culting. Pays cost, doesn't get benefit (because the benefit requires the underlying problem to exist).

**Instead**: name the *specific* problem you're solving. If you can't, default to modular monolith.

## No idempotency on state-changing calls

**Spot it**: payment endpoint takes a request, returns a response, that's it. No idempotency key. No way to safely retry.

**Why bad**: network blips → duplicate charges, duplicate orders, duplicate emails. Real production incidents have cost real money over this (Uber Eats India incident is the canonical example).

**Instead**: idempotency keys on every state-changing call. Server stores key→result for a retention window. Repeats return original result.

## Observability as afterthought

**Spot it**: production system with print statements, no structured logs, no metrics, no traces. Debugging requires SSH into instances and tailing files.

**Why bad**: "we'll add observability later" never happens. When you need observability is during an outage; that's not the time to add it.

**Instead**: observability from day one. Structured logs, metrics (RED method: rate, errors, duration; or USE: utilization, saturation, errors), distributed traces. OpenTelemetry is the converging standard.

## Auth rolled by hand

**Spot it**: custom session token format, password hashing using SHA-1, JWT with `none` algorithm allowed, "we built our own auth."

**Why bad**: auth is hard to get right; many ways to fail; failures are catastrophic and often invisible until exploited.

**Instead**: OAuth 2.1, OIDC, or established providers (Auth0, Cognito, Clerk, Supabase Auth). For B2B SAML. Don't roll your own.

## Sharing models across service boundaries

**Spot it**: shared library / shared package containing data models that all services import. Schema change in the library forces every service to re-deploy.

**Why bad**: defeats the purpose of service boundaries. Tight coupling through the shared model.

**Instead**: each service owns its model. Translate at the boundary (DTOs, anti-corruption layers). Yes, this means duplication. The duplication is the price of independence.

## Event sourcing for everything

**Spot it**: applying event sourcing to every domain in the system, regardless of whether the domain has a meaningful event stream.

**Why bad**: event sourcing is powerful but has high complexity cost (replay, projection, schema evolution, debugging). Inappropriate for CRUD domains where events are just "field X was updated."

**Instead**: event sourcing where the event stream *is* the natural model (commerce orders, accounting ledger, audit logs, IoT telemetry). Boring CRUD elsewhere.

## Distributed tracing without sampling strategy

**Spot it**: 100% trace sampling at scale → trace storage costs explode → team turns it off → no traces when needed.

**Why bad**: all-or-nothing observability is brittle.

**Instead**: head-based sampling for normal traffic (1-5%), tail-based sampling for errors (100%), context-aware (always sample slow requests).

## "We'll fix this in v2"

**Spot it**: known architectural problem with a deferred fix, but no concrete plan, no owner, no deadline.

**Why bad**: v2 doesn't ship. The compromise becomes permanent.

**Instead**: either fix it now, or write it down explicitly with owner + trigger condition for revisit.

## How to use this in consultations

When recommending a direction, also flag the 2-4 anti-patterns the user is most likely to hit on that direction.

- Recommending modular monolith → flag "module boundary discipline" risk
- Recommending microservices → flag distributed monolith, premature distribution
- Recommending event sourcing → flag "for everything" and projection complexity
- Recommending caching → flag invalidation and stale-read risk
- Recommending custom auth → flag the entire category; redirect to standard providers

Don't lecture. Pick the 2-4 most relevant to the proposed direction and call them out concretely.
