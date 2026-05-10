# Cost Anchors

Rough monthly $$ ranges for common architectures at common scales. **Anchors, not quotes.** Real costs vary 3-10× by region, vendor, and discipline. Use to ground the operability bar; flag when a user's constraint is wildly off.

All figures USD per month, list price, common cloud (AWS/GCP/Azure), 2026 baseline. For Singapore/Bangkok/Sydney regions, multiply by ~1.1-1.3 for compute, ~1.5-2× for egress. Reserved instances / savings plans cut compute 30-50%.

## Pre-product / hobby (≤100 MAU, ≤10 RPS)

- Managed platform (Railway, Fly.io, Render, Vercel hobby): **$0-30/mo**
- Plus managed Postgres: **$5-25/mo**
- Plus Sentry/UptimeRobot free tiers: **$0**
- **Total: $5-50/mo**

If a hobby project is costing >$100/mo, something is wrong (idle resources, wrong tier, or accidentally provisioned cluster).

## Early users (1k-10k MAU, 10-100 RPS)

- Single small VM or container (2 vCPU, 4GB RAM): **$25-75/mo**
- Managed Postgres (small, 2 vCPU): **$50-150/mo**
- Redis (small): **$15-50/mo**
- CDN (Cloudflare Free / Bunny / CloudFront): **$0-30/mo**
- Logs + metrics (managed, e.g., Better Stack, Grafana Cloud free): **$0-50/mo**
- Error tracking (Sentry team): **$0-30/mo**
- Email/SMS (transactional): **$10-50/mo**
- **Total: $100-400/mo** for a typical SaaS at this stage

Microservices at this stage: **$500-2000/mo** for the same workload. Often the wrong call.

## Scaling (10k-100k MAU, 100-1k RPS)

- App tier (3-5 instances, autoscaled): **$200-800/mo**
- Postgres (medium, with read replica): **$300-1000/mo**
- Redis (production tier): **$100-400/mo**
- CDN + WAF: **$50-300/mo**
- Observability stack (Datadog/New Relic/Honeycomb): **$200-1500/mo** — this is often surprisingly large
- Background jobs (workers, queues): **$100-400/mo**
- Object storage (S3/GCS, with traffic): **$50-300/mo**
- **Total: $1k-5k/mo** for a healthy single-region monolith / modular monolith

Microservices equivalent: **$3k-15k/mo** plus 1-2 platform engineers ($140k-360k/yr in salary).

## Mature (100k-1M MAU, 1k-10k RPS)

- Compute tier (autoscaled, multi-AZ): **$2k-15k/mo**
- Postgres (large, read replicas, possibly sharded): **$2k-20k/mo**
- Caching layer: **$500-3k/mo**
- CDN + edge: **$200-2k/mo**
- Observability (logs alone often $1k-10k/mo at this scale): **$2k-15k/mo**
- Background processing: **$500-3k/mo**
- Storage + egress: **$500-5k/mo**
- **Total: $10k-50k/mo** for a healthy modular monolith with selective service extraction
- Multi-region multiplier: 1.5-2.5×

Microservices at this scale: **$30k-150k/mo** plus 3-8 platform engineers. Justified if independent scaling / regulatory / polyglot needs are real.

## Cost surprises (the silent killers)

Watch for these — they routinely 3-10× a budget:

- **Egress** — cross-AZ chatter, region-to-region replication, internet egress without CDN. Easy to hit $2k-10k/mo unexpectedly.
- **Logs** — high-cardinality logs at high volume on Datadog/Splunk. Easy to hit $5k-20k/mo. Sample aggressively.
- **Idle Kubernetes** — clusters provisioned for peak, running 24/7. Easy to hit $1k-5k/mo of pure waste.
- **Forgotten environments** — staging/preview environments that no one uses but no one shut down.
- **Backup storage** — long-retention backups at high frequency. Lifecycle policies fix this.
- **Snapshots** — EBS snapshots accumulate. Same as backups.
- **Distributed tracing at 100% sample rate** — easy $5k-30k/mo at scale. Tail-based sampling for errors only is usually right.
- **Per-request paid services** (some auth providers, payment APIs) — model the cost per user before committing.

## Per-user economics (rough)

For a typical SaaS at scale (100k-1M MAU):
- $0.05-0.50 / MAU / month is healthy
- $0.50-2.00 / MAU is acceptable for high-touch or data-heavy products
- $2+ / MAU should be justified by ARPU; otherwise the architecture is wrong

For a side project:
- $0.10-1.00 / MAU is acceptable since fixed costs dominate at low scale

## How to use this in consultations

When asked to estimate operability cost:
1. Anchor to a tier (pre-product / early / scaling / mature) based on user's stated scale
2. Quote the range, not a point estimate
3. Flag the surprises if the architecture has any (microservices premium, observability at scale, multi-region, egress)
4. If user's stated budget is wildly off (e.g., wants Netflix-grade for $50/mo), name the gap explicitly

Don't manufacture precision. "Roughly $200-500/mo for the early-users tier" is more honest than "$347/mo."

## When in doubt

Ask the user to run their actual numbers through cloud calculators (AWS Pricing Calculator, GCP Pricing Calculator) for their specific region. These anchors are for sanity-checking direction, not for building a budget.
