# Scaling Diagnostics — Hypothesis Trees

## Use this when

User says: "we're slow", "costs are exploding", "we keep hitting timeouts", "things broke when we grew", or any other symptom-shaped scaling complaint.

The job is *not* to recommend a fix immediately. It's to:
1. Form a hypothesis tree of what could cause this class of symptom
2. Tell the user what to measure to discriminate between hypotheses
3. Then recommend fixes ranked by likelihood × cost-to-implement

Symptom → measurement → fix. In that order.

## Symptom: high latency

### Hypothesis tree
- **Database-bound**
  - Slow queries (missing indexes, N+1)
  - Lock contention
  - Connection pool exhaustion
  - Database CPU/memory saturation
- **Network-bound**
  - Sync call chains across many services
  - Cold cross-region calls
  - DNS resolution issues
  - TLS handshake overhead (no connection reuse)
- **Compute-bound**
  - CPU saturation on app servers
  - Memory pressure / GC pauses
  - Single-threaded bottleneck
- **External-dependency-bound**
  - Slow third-party API
  - Rate-limiting from upstream
- **Tail-latency specific**
  - GC pauses (JVM/Go), p99 spikes
  - Cold caches
  - Noisy neighbor on shared infra

### What to measure first
- p50, p95, p99 latency, broken down by endpoint
- Database query times (slow query log)
- Per-service timing (distributed traces)
- CPU/memory utilization on app servers and database
- Connection pool stats

### Common fixes by ROI
1. Add missing database indexes (cheapest, highest impact)
2. Eliminate N+1 queries
3. Add caching layer (Redis) for hot reads
4. Increase connection pool size or add PgBouncer
5. Vertical scale the database
6. Read replicas for read-heavy workloads
7. Async-ify non-critical operations
8. Sharding (last resort, most expensive)

## Symptom: cost growth outpacing user growth

### Hypothesis tree
- **Idle infrastructure**
  - Over-provisioned instances
  - Idle Kubernetes clusters
  - Forgotten test environments
  - Unused storage / snapshots
- **Inefficient compute**
  - Wrong instance types (compute-optimized for memory-bound work)
  - No autoscaling, sized for peak
  - Oversized containers
- **Storage**
  - No lifecycle policies (logs growing forever)
  - High-tier storage for cold data
  - Cross-region replication when not needed
- **Network egress**
  - Cross-AZ chatter
  - Data transfer to other regions
  - Egress to internet (CDN miss, no caching)
- **Microservices premium**
  - Service mesh overhead
  - Per-service idle cost
  - Observability stack at scale

### What to measure first
- Cost breakdown by service / tag / team (FinOps)
- Utilization rate per instance (idle vs. busy)
- Egress cost as % of total
- Cost per request / per user

### Common fixes by ROI
1. Right-sizing (down-sizing instances to match actual usage)
2. Spot instances for non-critical batch
3. Reserved instances / savings plans for steady baseline
4. Storage lifecycle policies (move cold data to cheaper tiers)
5. CDN for static and cacheable dynamic content
6. Consolidate microservices that don't need to be separate
7. Egress audit — keep traffic within AZ where possible

## Symptom: we keep hitting timeouts / cascading failures

### Hypothesis tree
- **Missing resilience patterns**
  - No timeouts (waiting forever)
  - No circuit breakers (thundering herds)
  - No bulkheads (one bad service exhausts all)
  - Naive retries (amplifying load on already-struggling services)
- **Cascading dependency**
  - Sync chains too long
  - Single-point-of-failure dependency
  - No graceful degradation
- **Capacity / scaling**
  - Autoscaling too slow to react
  - Hot spots in sharded systems
  - Connection limits hit before CPU/memory

### What to measure first
- Error rate per service, per endpoint
- Latency at each hop (distributed traces)
- Connection pool utilization
- Retry counts and timeout occurrences

### Common fixes by ROI
1. Add explicit timeouts everywhere
2. Add circuit breakers between services
3. Add idempotency keys (so retries are safe)
4. Bulkhead connection pools per downstream
5. Async-ify non-critical chains
6. Add graceful degradation paths
7. Pre-warm caches / autoscaling

## Symptom: database is the bottleneck

### Hypothesis tree
- **Read-heavy** → caching, read replicas
- **Write-heavy** → sharding, CQRS, event sourcing
- **Both** → re-evaluate workload split, consider polyglot persistence
- **Hot keys** → keyspace redesign or distributed cache layer
- **Schema-shape mismatch** → wrong DB type for access pattern (using SQL for graph traversals, etc.)

### What to measure first
- Read/write ratio
- Top-N slow queries
- Hottest rows / keys
- Lock contention metrics

### Common fixes by ROI
1. Indexes on hot queries
2. Application-level caching (Redis)
3. Read replicas
4. Materialized views for expensive reads
5. Move write-heavy workloads to a queue → async write
6. Sharding (only when above options exhausted)

## Symptom: deployments are slow / risky

This is often misdiagnosed as a tooling problem when it's actually an architecture problem.

### Hypothesis tree
- **Monolith too coupled** → can't deploy any change without testing everything
- **Microservices too coupled** (distributed monolith) → need to deploy services in lockstep
- **Insufficient test coverage** → deploys are scary because nothing's verified
- **No canary / no rollback strategy** → every deploy is all-or-nothing
- **Long CI pipelines** → slow feedback loop

### Common fixes
1. Feature flags (decouple deploy from release)
2. Canary deploys / blue-green
3. Test pyramid (more unit/integration, fewer slow E2E)
4. Modular boundaries (so deploys don't have to test the whole world)
5. Trunk-based development with short-lived branches

## How to use this in a consultation

1. Listen for the symptom
2. Walk the relevant hypothesis tree out loud (or ask clarifying questions to narrow)
3. Recommend what to measure first (don't recommend fixes blind)
4. Once measurements are in, recommend fixes ranked by ROI
5. Flag the cheap-but-overlooked options first (indexes, caching, right-sizing)
6. Save expensive options (sharding, microservices, rewrites) for last
