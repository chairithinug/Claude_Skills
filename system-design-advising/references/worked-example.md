# Worked Example — A Model Consultation

This is what good output looks like. Reference it when in doubt about output shape.

---

## User prompt (greenfield mode)

> I'm building a badminton court booking and game-scheduling app for the Bangkok market. Just me as the developer (with Claude Code). Expecting maybe 100 users in first 6 months, hopefully 1-2k by year end. Users register, see available courts, book time slots, invite friends to games, see ratings/skill-level matches. I'm comfortable with Python/TypeScript, want to keep monthly costs under $50 if possible.

## Model response

**Mode**: greenfield

**Diagnosis**

This is a small-team / pre-product greenfield with hard cost constraint. The load-bearing pillars are **maintainability** (you're solo, future-you needs to read this code), **cost** (under $50/mo cap is real), and **change velocity** (you don't yet know what users want — you'll iterate). Scalability and reliability are *not* load-bearing yet — 1-2k users is well within single-instance territory. This means the architecture should optimize for getting to feedback fast and being cheap to run, not for theoretical future scale.

**Context check**

Stating these assumptions; correct any that are wrong:
- Single region (Singapore region for low Thai latency, ~30-50ms to BKK)
- No regulatory complexity beyond basic Thai PDPA (if you collect PII, you'll need a privacy notice; not architecturally significant at this scale)
- This will be web-first; mobile may come later
- You want to ship within weeks, not months

**Recommendation**

A **modular monolith** on a managed platform. Concretely:

- **Stack**: TypeScript (Next.js full-stack) or Python (FastAPI + a JS frontend). Pick the one you'd ship faster in. Both are fine. *(Trade-off: TypeScript means one language end-to-end; Python may feel more natural if you think in scripts. Either is correct here.)*
- **Hosting**: Fly.io Singapore region (`sin`) or Railway. Both deploy via git push, both around $5-10/mo for a small instance. *(Trade-off vs. Vercel: Vercel is great for Next.js but pricing on backend usage gets unpredictable; Fly/Railway are more predictable for small full-stack apps.)*
- **Database**: Managed Postgres on the same platform (Fly Postgres or Railway Postgres), ~$5-15/mo for a small instance. *(Trade-off vs. SQLite: Postgres is strictly better here once you have multi-user state; SQLite is for single-user or content sites.)*
- **Auth**: Don't roll your own. Use Clerk or Supabase Auth (free tier covers 2k users easily) or your own bcrypt + JWT if you really want hands-on. *(Trade-off: Clerk is fastest; Supabase gives you DB + auth bundled; rolling your own takes a weekend you could spend on features.)*
- **Background jobs**: Skip a job queue at this scale. If you need scheduled work (sending reminders, computing matches), use a single cron-style worker on the same instance. Add a queue (Redis + BullMQ) only when you have evidence you need one.
- **No CDN, no microservices, no Kubernetes, no message queue, no Redis**. You don't need them. They will appear when you actually have a problem they solve.

**Trade-offs and flip conditions**

What this design costs: scaling ceiling at single-instance Postgres (~10k-50k MAU, depending on access patterns), no zero-downtime deploys (tolerable at this scale — deploy at 4am Bangkok time), single region (latency for non-Thai users will be worse).

What would flip the recommendation:
- If you suddenly hit 50k+ MAU → split read replicas, add Redis cache, evaluate splitting the matchmaker into a worker
- If you take VC funding and hire 5+ engineers → modular monolith still right, but invest in observability + CI/CD discipline earlier
- If you go multi-country with low-latency requirements → consider edge compute or multi-region (but probably not for years)
- If you collect health/identity data → PDPA + possibly health-data rules, and that changes the data layer

**Anti-patterns to avoid**

- **Premature distribution**: don't split into "user service / booking service / notification service." You will regret it. Single codebase, modular folders.
- **Custom auth**: don't write your own login flow. Use a provider.
- **Database-as-API**: don't expose Postgres directly to the frontend (Supabase RLS is a *managed* version of this and OK; raw direct access is not).
- **No idempotency on booking endpoint**: bookings are state-changing money-adjacent operations. Use an idempotency key from the client (UUID); reject duplicate requests within 24h. This costs ~10 lines of code and prevents double-booking on network blips.

**Operability bar**

- **Deploy**: git push → platform builds → deploys. Both Fly and Railway do this. Rollback is one command. Set up basic CI (GitHub Actions running tests before deploy).
- **Observability**: structured logs to platform's log viewer (free), Sentry free tier for error tracking (covers 5k events/mo), UptimeRobot free for uptime monitoring. That's enough for this stage.
- **On-call**: you are on-call. Add a Telegram or LINE webhook for Sentry alerts so you see them on your phone.
- **Cost**: budget $10-30/mo realistic. Fly small instance ($5) + Postgres ($5-15) + Sentry free + UptimeRobot free + domain ($10/yr). Comfortably under your $50 cap.

**Open questions**

- Are users paying? If yes, payment provider choice (Stripe in Singapore covers Thailand; Omise is Thai-native and supports PromptPay) is the next decision.
- Court inventory — do you own this data, or are you scraping/integrating with court operators? This shapes the data model significantly.
- Skill-rating system — a simple Elo or Glicko? This is a fun model decision; doesn't affect architecture much.

If useful, I can drill into (1) **the data model** for users / courts / bookings / games / ratings (~30-min sketch), (2) **the matchmaker logic** for skill-based pairing (Elo vs. Glicko vs. simpler heuristics), or (3) **the payment flow** if you're charging — including Thai-specific options like PromptPay via Omise.

---

## What this example demonstrates

- **Diagnosis names load-bearing pillars first** (maintainability, cost, velocity), explicitly excludes ones that aren't (scalability, reliability not yet).
- **Context check states assumptions** rather than asking 6 questions.
- **Recommendation is layered** (stack, hosting, database, auth, jobs) with trade-offs inline.
- **Trade-offs are concrete** ("scaling ceiling at ~10k-50k MAU"), not vague.
- **Flip conditions are specific** ("if you hit 50k+ MAU…").
- **Anti-patterns are proximate to the recommendation** (the user is going to be tempted by premature distribution or custom auth at exactly this stage).
- **Operability bar is actionable** with specific tools and concrete dollar figures.
- **Closing offer is concrete and tied to user's situation** (Thai payment options, badminton matchmaker logic).
- **No canned best-practice list.** Every recommendation is connected to "for your scale and constraint."
- **Length matches mode**: greenfield deep-dive, ~1100 words. A `quick` mode answer to the same question would be ~150 words and look very different.

## Anti-example (what NOT to do)

> "For a scalable web application, you'll want to consider a microservices architecture with a load balancer in front, separate services for users / bookings / notifications, a message queue for async work, Redis for caching, Postgres for primary data, ElasticSearch for search, observability via Datadog or New Relic, deployed on Kubernetes (EKS) with CI/CD via GitHub Actions, monitoring with Prometheus and Grafana…"

This is the canned best-practice dump. Every word might be technically defensible at *some* scale, but for a solo dev with 100 users and a $50/mo budget it is malpractice. It will:
- Cost $500-2000/mo to run
- Take months to set up before the first user can book a court
- Require ops knowledge the solo dev doesn't have
- Solve no problem the user actually has

If you find yourself producing this kind of response, **stop and re-read Step 1**.
