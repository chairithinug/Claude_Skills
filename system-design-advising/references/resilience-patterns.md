# Resilience Patterns

## The mindset

Failures are inevitable in any distributed system. The job is not to prevent them, it's to design *for* them so the system degrades gracefully instead of cascading.

Most resilience problems trace to missing one of: timeouts, retries, circuit breakers, idempotency, or graceful degradation. The patterns below are the toolkit; pick the ones that fit the failure modes you actually face.

## The patterns

### Timeouts (always)
Default network timeouts are usually wrong — too long, or absent. Set explicit timeouts on every external call:
- Database queries
- HTTP/gRPC calls to other services
- Cache lookups (yes, even cache)
- Message broker operations

Timeout shorter than the upstream caller's timeout. Timeouts compose: if A calls B calls C, A's timeout must be > B's > C's.

### Retries with exponential backoff + jitter
Naive retries cause thundering-herd outages. Always:
- Exponential backoff (1s, 2s, 4s, 8s...)
- Random jitter (multiply each delay by random 0.5-1.5)
- Cap on total retry count (typically 3-5)
- Cap on total elapsed time

Only retry idempotent operations, or operations protected by idempotency keys.

### Circuit breakers
When a downstream is failing repeatedly, stop hammering it. States:
- **Closed** — calls pass through; track failure rate
- **Open** — failure rate exceeded threshold; calls fail fast without hitting downstream
- **Half-open** — after cooling period, allow a few test calls; if they succeed, close; if fail, reopen

Prevents cascading failures and gives the downstream time to recover.

### Bulkheads
Isolate failure domains so one bad dependency can't sink the ship. Examples:
- Separate connection pools per downstream service (one slow service can't exhaust all connections)
- Separate thread pools for different work types
- Separate queues per consumer
- Separate Kubernetes pods / ASGs per critical workload

Named after ship bulkheads — flooding one compartment doesn't sink the ship.

### Idempotency
A request can be safely retried without duplicate side effects. Required for any state-changing call across an unreliable network.

Implementation: client generates an idempotency key (UUID), server stores key→result for some retention window. Repeat requests with same key return the original result instead of re-executing.

Critical for: payments, orders, account creation, anything financial.

### Graceful degradation
When something breaks, fall back to a degraded experience instead of returning 500.
- Recommendations service down → show generic content
- Personalization down → show defaults
- Search down → show recent items
- Cache miss in degraded mode → return stale cached data with a warning

Better than a blank page. Better than an error.

### Saga pattern (distributed transactions)
Two-phase commit doesn't scale. For multi-service workflows that need transactional semantics:
- Sequence of local transactions, each with a compensating action
- If step N fails, run compensating actions for steps 1...N-1 to undo
- Requires careful design — compensations aren't always perfect rollbacks

Use when you genuinely need distributed transactions. Often the right answer is "redesign the workflow to not need it."

### Health checks (multiple layers)
Different probes mean different things:
- **Liveness** — is the process alive? Restart if not.
- **Readiness** — is it ready to serve traffic? Remove from load balancer if not.
- **Startup** — has it finished initializing? Don't kill it during startup.

Bad health checks cause more outages than they prevent. Make them check what actually matters (can the service do its job), not trivia.

### Backpressure
When a consumer can't keep up with a producer, signal upstream to slow down:
- Bounded queues (block or shed when full)
- Rate limiting at ingress
- Reactive streams patterns
- Token bucket / leaky bucket

Without backpressure, queues grow unbounded and the system OOMs or hits cascading timeouts.

### Chaos engineering (advanced)
For systems where failures are expensive enough to justify deliberate practice:
- Kill random instances in production (Netflix's Chaos Monkey)
- Inject network latency
- Simulate downstream failures
- Run regular game-days

Useful at scale. Overkill for small teams.

## Common gaps to flag in reviews

When reviewing an existing design, check for these missing pieces:
- No timeouts → guaranteed cascading failure on first slow downstream
- Naive retries → thundering herd waiting to happen
- No idempotency → guaranteed duplicate orders/charges/messages on first network blip
- No circuit breakers in microservices → one slow service brings down everything calling it
- No bulkheads → one bad downstream exhausts all connection pools
- No graceful degradation → 500s instead of degraded UX
- 2PC distributed transactions → won't scale, refactor to saga
- Sync chains 5+ services deep → tail latency multiplication

## When NOT to add resilience patterns

Resilience patterns have cost:
- Complexity
- Cognitive load
- Bugs in the resilience layer itself

For a single-process application with no remote calls, most of this doesn't apply. Don't add circuit breakers between modules in the same process. Don't add idempotency keys to local function calls.

Match the pattern to the failure mode you actually have.
