# API Protocol Decision Matrix

## The 2026 consensus

There is no single "best" API protocol. Modern systems use multiple protocols at different boundaries. The pattern that wins:
- **Internal service-to-service**: gRPC (binary, fast, typed)
- **Edge / client-facing**: REST or GraphQL (depending on client diversity)
- **Public / partner**: REST (broad compatibility, HTTP caching)
- **Async / decoupled**: message queues / event streams

The choice for each boundary depends on the *boundary's* constraints, not on a global protocol decision.

## The matrix

| Boundary | First choice | When to pick it | When NOT to |
|----------|--------------|-----------------|-------------|
| Public / partner API | REST | Default; broad compatibility, HTTP caching, debuggable | When clients have radically varied data needs |
| Public / mobile + web + partner | GraphQL | Heterogeneous clients with varied data shapes; reduce over/under-fetching | Single client type; CRUD-heavy; small team without GraphQL experience |
| Internal service-to-service | gRPC | Latency-sensitive, high throughput, polyglot services with shared schemas | Browser-to-service (use gRPC-Web or REST instead); team without protobuf comfort |
| Full-stack TypeScript | tRPC | End-to-end type safety, no codegen, single team owns front + back | Polyglot stack; public API; large org with multiple language clients |
| Real-time bidirectional | WebSockets | Chat, collab, live game state, multiplayer | Server-to-client only (use SSE); request-response (use REST/gRPC) |
| Server-to-client push | Server-Sent Events | Notifications, progress updates, dashboards | Bidirectional needs; binary data |
| Async / event-driven | Message queues (SQS, RabbitMQ) | Decoupling, load smoothing, fan-out, retry semantics | Synchronous request-response needs |
| Event streaming / replay | Kafka / Pulsar | Event sourcing, audit, replay, multiple consumers, ordered streams | Simple async (queues are simpler); low volume |
| AI agent / tool calling | MCP (Model Context Protocol) | LLM-callable tools, schema discovery, typed inputs/outputs | Non-LLM clients; norms still settling — likely complement to REST/gRPC |

## Hygiene that matters more than protocol choice

- **Idempotency keys** for any state-changing call. Non-negotiable for payments, orders, anything financial. Missing this has caused real production incidents (Uber Eats India, others).
- **Versioning from day one** — URL path (`/v1/`) or header. Plan for deprecation timelines.
- **Resource-oriented URLs** for REST: nouns plural, hierarchy follows ownership. `/users/123/orders`, not `/getUserOrders?id=123`.
- **Correct HTTP semantics**: GET safe and idempotent, PUT idempotent, POST not, DELETE idempotent. Use status codes properly.
- **OpenAPI / Protobuf / GraphQL schema** as single source of truth; generate clients and docs.
- **Auth**: OAuth 2.1, API keys, or mTLS. Don't roll your own.
- **Rate limiting + quotas** at the edge.
- **TLS everywhere**, including internal calls.

## Common decision patterns

### "We need an API for our mobile app and web app"
→ REST first if data shapes are similar across clients. GraphQL if they differ substantially (mobile needs minimal, web shows everything).

### "We're splitting our monolith into services and need them to talk"
→ gRPC for the internal calls, keep REST at the public edge. Don't expose gRPC directly to browsers.

### "We need real-time updates"
→ Direction matters. Server-to-client only: SSE (simpler). Bidirectional: WebSockets.

### "We have a payment / order system"
→ Whatever protocol, idempotency keys are mandatory. Design the key generation strategy upfront.

### "We want LLMs to call our APIs"
→ MCP is emerging as the standard for tool-calling. Maintain REST/gRPC alongside; MCP is a complement, not a replacement. Norms still settling — be conservative.

### "We have webhooks / partner notifications"
→ REST POST with HMAC signing. Provide a replay/retry mechanism on the consumer side.

## Anti-patterns

- **GraphQL because Facebook uses it** — without heterogeneous clients, you pay complexity tax for no benefit.
- **gRPC at the public edge** — browsers don't speak it natively; gRPC-Web adds a proxy.
- **REST APIs that ignore HTTP semantics** — POST for everything, custom status codes, query params for everything. Loses caching and tooling benefits.
- **No versioning** — first breaking change becomes a crisis.
- **Sync chains across many services** — each hop multiplies tail latency. Use async or compose at the edge.
- **Database-as-API** — exposing raw SQL or direct DB access across service boundaries. Couples consumers to internal schema.
