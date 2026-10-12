# Architecture, Reliability & Load-Test Evidence

Use this reference when a project has meaningful backend traffic, stateful workflows, expensive operations, realtime updates, uploads, or reliability requirements. It is not a mandate to add infrastructure. Choose the simplest architecture that meets verified product needs.

## 1. Measure before scaling

- Define representative user journeys and the mix of reads, writes, searches, uploads, background jobs, and AI calls.
- Use realistic data volume, payload sizes, authentication, cache state, and user think-time. A tight synthetic loop can differ greatly from real usage.
- Test a baseline, ramp-up, expected peak, short spike, and sustained/soak period when justified.
- Record throughput, p50/p95 latency and p99 where appropriate, error/timeout rate, CPU, memory, database connection use, slow queries, queue lag, and relevant provider/model spend.
- Monitor the load generator. If it saturates first, the test does not prove the application's capacity.
- Set pass/fail thresholds from product SLOs, user expectations, and budget. Do not copy arbitrary benchmark numbers or claim a user capacity from one screenshot.
- Use a controlled environment and limits that will not overload production or create unexpected charges. Test the production build and realistic deployment configuration.

Record workload, environment, duration, cache state, bottleneck, thresholds, and test output. A load test without a representative workload and acceptance criteria is weak evidence.

## 2. Scale in response to evidence

Prefer the smallest architecture that meets the requirement. Add a layer only when a measured bottleneck, availability requirement, or product feature justifies its complexity.

- **One application instance:** acceptable for many small products when availability and resource limits match the need.
- **Load balancer / multiple instances:** verify health/readiness checks, draining during deploys, and behavior when an instance is unhealthy.
- **Connection pooling:** check pool size against database limits and application concurrency. Oversized pools can exhaust the database; undersized pools can create avoidable queueing.
- **Read replicas:** document replication lag and behavior when a user expects to read their own recent write.
- **Sharding:** a high-complexity option. Require evidence that simpler indexing, query design, caching, partitioning, or read scaling cannot meet the need. Check hot shards, shard-key distribution, cross-shard queries, and rebalancing/migration plans.
- **Object storage + CDN:** consider for user-uploaded media and large files. Verify access controls, signed URL expiry, cache headers, deletion behavior, and origin protection.
- **Queues/workers:** define queue limits, retry policy, idempotent handlers, poison-message/dead-letter handling, lease/visibility timeouts, queue-lag alerts, and recovery/replay procedures.
- **Redundancy/failover:** identify single points of failure that conflict with availability needs. Verify failover rather than assuming a second instance proves resilience.
- **Observability:** ensure actionable logs, metrics, traces where useful, alert ownership, and runbooks. Avoid logging secrets or unnecessary personal data.

Do not introduce Kubernetes, microservices, sharding, Redis, or a load balancer solely because a tutorial uses them. Account for operational cost, deployment complexity, failure modes, and maintainability.

## 3. Cache correctness, not just cache speed

For every cache, identify the source of truth, key, TTL/invalidation strategy, consistency requirement, and failure behavior.

- Include tenant/user/authorization scope, locale, query parameters, or content version in keys when they affect results.
- Never let a shared cache serve one user's private response to another. Verify CDN and reverse-proxy cache headers for authenticated responses.
- Test stale reads after create/update/delete, permission changes, logout, account switching, and tenant switching.
- Treat TTL as a bounded-staleness policy, not a substitute for deliberate invalidation.
- Consider cache stampedes on expiry or outage; use proportionate request coalescing or jittered expiry when justified.
- Test cold and warm cache behavior. A cache outage must not trigger an unbounded database/provider surge.
- Compare strategies against actual requirements:
  - **Cache-aside:** application loads on a miss; invalidation and concurrent updates still need thought.
  - **Write-through:** verify partial-failure behavior across cache and source of truth.
  - **Write-behind:** writes may be acknowledged before durable persistence. Use only when the tolerated loss window is explicit and recovery, ordering, retries, and idempotency are tested.
- Do not add a cache merely to improve a benchmark if correctness, privacy, or cost suffers.

## 4. Retry, timeout, and failure containment

- Set explicit timeouts for outbound HTTP, database, model, and other network calls.
- Bound retry attempts and total retry time. Use exponential backoff with jitter for retryable transient failures where appropriate.
- Retry only operations safe to repeat or protected by idempotency keys/operation identifiers. Do not blindly retry payments, messages, emails, or writes.
- Avoid retry multiplication across clients, services, SDKs, workers, and gateways. Establish which layer owns retries.
- Use circuit breakers or concurrency bulkheads when they prevent a failing dependency from exhausting the whole service; test recovery behavior.
- Test graceful worker shutdown and deployment behavior so in-flight work is completed, retried safely, or explicitly recovered.

## 5. Realtime transport selection and safety

Choose transport based on interaction requirements rather than novelty.

- **WebSockets:** ongoing bidirectional communication.
- **Server-Sent Events (SSE):** server-to-client streaming when client actions can use normal HTTP.
- **Polling:** may suffice for low-frequency updates when simpler operations are preferable.

For realtime endpoints, verify:
- authentication at connection time and authorization for every channel, room, topic, or subscribed resource
- origin policy and safe cookie/token handling; avoid secrets in URLs that may be logged
- bounded message size, connection count, per-user subscriptions, outbound buffers, and message-processing work
- heartbeat/idle timeout and disconnected-client cleanup
- reconnect with backoff/jitter, and replay/resume semantics when missed events matter
- duplicate, delayed, or out-of-order event handling when ordering matters
- multi-instance fanout and coordination between workers
- safe behavior during deploys, outages, and expired sessions

Test disconnections, reconnects, stale sessions, unauthorized subscriptions, and sustained message volume. A local demo updating instantly is not proof of reliable realtime delivery.

## 6. Launch economics and third-party dependencies

- Inventory relevant recurring/per-action costs: hosting, database, storage, bandwidth, email/SMS, AI inference, analytics, domain, app-store, and paid third-party services.
- Verify whether a paid service, developer program, custom integration, or premium model is actually required; check current pricing, eligibility, terms, and platform rules before spending.
- For AI features, measure prompt/context size, repeated calls, model choice, output limits, caching eligibility, retries, and cost per representative workflow. Do not send the entire conversation or database by default.
- Define upload size/count quotas, retention, deletion behavior, and storage growth monitoring.
- Distinguish alerts from hard caps and automatic pauses.
- Test behavior when provider quota, budget, rate limit, or billing state is reached. Avoid accidental free access to paid features.

Do not invent cost estimates. Use actual pricing and workload assumptions, and label projections as estimates.

## 7. AI workflow reliability and decision quality

For AI-assisted products or agent workflows that classify, route, triage, score, retrieve, escalate, or call tools, check more than prompt-injection security. A workflow can be secure and still make unreliable or expensive decisions.

- Define the job, accepted inputs, expected output schema, and what the system must do when it cannot decide.
- Validate and normalize inputs before model calls. Validate structured model outputs against a schema before they affect state or trigger downstream actions.
- Treat retrieved documents as untrusted evidence. Check relevance, freshness, tenant/permission filtering, duplicate content, and whether the system can abstain when retrieval is weak.
- Use deterministic rules for simple, high-confidence checks where they are more reliable and cheaper than a model. Use model routing only when the task, latency, quality, and cost tradeoff is justified.
- For spam detection, ticket classification, support triage, lead scoring, request routing, and similar decisions, define false-positive and false-negative costs and test representative examples.
- Define confidence/uncertainty behavior: retry with a changed strategy only when useful, ask a clarifying question, abstain, or escalate to a human. Do not fabricate certainty.
- Restrict tool selection to an allowlist and validate every tool argument server-side. The model must not choose its own authority or bypass application authorization.
- Make side-effecting tools idempotent where possible. Bound retries and prevent duplicate emails, payments, tickets, records, or notifications.
- Keep a small, versioned evaluation set covering normal cases, edge cases, adversarial inputs, ambiguous cases, and known failures. Compare quality, latency, and cost when prompts, models, retrieval, or routing change.
- Log enough sanitized decision metadata to debug routing and failures, without storing secrets, full sensitive prompts, or unnecessary personal data.
- Monitor escalation rate, override rate, incorrect classifications, retry frequency, token use, and cost per successful workflow. Alert on meaningful regressions.
- Provide a manual fallback for high-impact decisions or when the model/provider is unavailable. Do not let an uncertain model decision silently grant access, charge a user, or perform an irreversible action.

## 8. Evidence and further reading

For each relevant check, use PASS only with concrete code/configuration/test/metric evidence; use FAIL when evidence shows a missing or broken control; use UNKNOWN when production/provider behavior cannot be verified; use NOT APPLICABLE only when genuinely irrelevant. Separate a configured control from a successfully exercised recovery procedure.

- [Google SRE Book](https://sre.google/sre-book/table-of-contents/) — reliability engineering, monitoring, overload, and incident response.
- [Grafana k6: thresholds](https://grafana.com/docs/k6/latest/using-k6/thresholds/) — measurable pass/fail criteria for load tests.
- [AWS Builders' Library: timeouts, retries, and backoff with jitter](https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/) — retry and timeout failure modes.
- [Redis: cache-aside pattern](https://redis.io/docs/latest/develop/use/patterns/cache-aside/) — caching behavior.
- [MDN: WebSocket API](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API) — bidirectional realtime communication.
- [MDN: Server-sent events](https://developer.mozilla.org/en-US/docs/Web/API/Server-sent_events) — server-to-client streams.
- [GitLab: Postmortem of database outage of January 31](https://about.gitlab.com/blog/postmortem-of-database-outage-of-january-31/) — destructive operational actions and unverified recovery assumptions.
