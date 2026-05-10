# Operability Checklist

Every architectural recommendation must answer these questions. If it doesn't, the recommendation is incomplete.

The Ivory Tower Architect failure mode is producing designs that look elegant but can't be operated. This checklist is the antidote.

## The four questions

### 1. How will this be deployed?

- CI/CD pipeline: what triggers a deploy, what gates exist (tests, security scans, manual approval)
- Deploy strategy: rolling, blue-green, canary, feature flags
- Rollback strategy: how do we undo a bad deploy, in how many minutes
- Database migration strategy: how do schema changes ship without downtime
- Configuration management: env vars, secrets store, config-as-code

If the answer is "we'll figure it out later" — flag it. The deploy story shapes everything.

### 2. How will we know it's broken?

The three pillars of observability:

**Logs** — structured (JSON), centralized, searchable, with retention policy. Not stdout dumps to a file.

**Metrics** — at minimum:
- RED method for services: Rate (RPS), Errors (error rate), Duration (p50/p95/p99 latency)
- USE method for resources: Utilization, Saturation, Errors
- Business metrics: orders/sec, signups/hour, revenue/day

**Traces** — distributed tracing (OpenTelemetry is the converging standard). Sample at a rate the team can afford.

**Alerting** — on SLO violations, not on individual metrics. Pager-worthy alerts must be actionable. Alert fatigue degrades the team faster than the underlying problems do.

**Dashboards** — one "is everything OK" dashboard per service, plus drill-downs.

### 3. Who's on-call and what's the runbook?

- Who carries the pager (rotation schedule)
- Who's the secondary / escalation
- For each pager-worthy alert: a runbook with steps to investigate and mitigate
- Post-incident: blameless review, action items tracked
- On-call burden estimate: how many pages per week is acceptable; if you exceed it, fix the system

If a system has no on-call, it has no production support. Either someone owns it or it doesn't really run.

### 4. What's the rough monthly cost at expected load?

- Compute (instances, containers, functions)
- Storage (databases, object storage, backups)
- Network (egress is the silent killer)
- Observability stack (logs, metrics, traces all cost real money at scale)
- Third-party services (auth, payments, email, etc.)
- Platform engineering people-cost (often dwarfs infrastructure cost)

Order of magnitude is fine for early-stage. "We have no idea" is not.

## SLI / SLO / SLA discipline

Different things, often confused:

- **SLI** (Service Level Indicator) — a measurement (e.g., p99 latency = 250ms)
- **SLO** (Service Level Objective) — a target you commit to internally (e.g., 99.9% of requests under 500ms over 30 days)
- **SLA** (Service Level Agreement) — a contract with consequences (e.g., refund if uptime falls below 99.95%)

Most teams need SLOs internally before promising SLAs externally. SLOs are how you decide what to invest in (error budgets, prioritization).

## Deployment patterns by maturity

**Level 0** — manual deploys, direct SSH, no rollback story. **Unacceptable** for production.

**Level 1** — automated CI, deploys via script, can rollback by re-deploying previous version. **Acceptable** for early stage.

**Level 2** — CI/CD with rolling deploys, feature flags for risky changes, monitoring catches regressions. **Healthy** for most teams.

**Level 3** — canary deploys, blue-green for risky services, automated rollback on SLO violation. **Right** for high-stakes systems.

**Level 4** — chaos engineering, deploy-on-merge, full automation. **Justified** at large scale.

Match the level to the stakes. Level 4 for a side project is overkill; Level 0 for a payment system is negligence.

## Common operability gaps to flag in reviews

When reviewing a design, check:
- [ ] Deploy story exists and someone owns the pipeline
- [ ] Rollback is tested, not just theoretical
- [ ] Structured logs centralized (not just stdout)
- [ ] Metrics include RED + USE
- [ ] Distributed traces in place (or planned)
- [ ] Alerts are actionable, not noise
- [ ] On-call rotation exists with secondary
- [ ] Runbooks exist for top-N alert types
- [ ] Cost estimate at projected load (within order of magnitude)
- [ ] SLO defined (even if internal-only)

If a design is missing 3+ of these, it's not production-ready. Name it.

## "Just enough" operability for stage

Don't demand Netflix-grade observability for a 100-user prototype. Match to stage:

**Pre-product** — basic logs (Heroku-style), uptime monitor (UptimeRobot), error tracking (Sentry).

**Early users** — structured logs, RED metrics, p99 latency tracked, on-call shared by 2-3 founders.

**Scaling** — proper observability stack (logs + metrics + traces), SLOs defined, rotation across the team.

**Mature** — full observability, error budgets, chaos engineering, multi-region.

Scale the operability investment with the system's stakes. But don't skip it entirely — even prototypes need to know when they're broken.
