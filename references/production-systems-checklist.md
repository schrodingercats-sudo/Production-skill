# Production Systems, Database & Operations Checklist

Use this reference to audit production systems beyond frontend polish. It expands the reliability audit into database correctness, distributed systems, delivery strategy, operations, networking, and incident response. Treat every item as conditional: inspect the actual stack and workload, mark genuinely irrelevant items NOT APPLICABLE, and do not add infrastructure just to satisfy a checklist.

## 1. Database performance and capacity

This section explicitly covers **database indexing**, **query optimization**, and **database migrations** as production checks, not merely code-style concerns.

- **Indexing:** inspect query plans and real query patterns before adding indexes. Check filtering, joins, ordering, composite-index order, selectivity, write amplification, index size, and unused/redundant indexes.
- **Query optimization:** inspect slow-query logs/plans, row estimates, scans, sort spills, lock waits, payload size, and query frequency. Optimize measured bottlenecks rather than guessing.
- **N+1 queries:** inspect loops, nested serializers, list/detail endpoints, and ORM relations for repeated round trips. Batch, join, eager-load, or otherwise reduce calls when correctness is preserved.
- **Connection pooling:** confirm pool size, acquisition timeout, idle/lifetime settings, and total connections across all app instances fit provider/database limits. Avoid opening a new connection per request.
- **Read replicas:** use only when read throughput warrants it. Verify replication lag, stale-read tolerance, read-after-write requirements, failover behavior, and that writes never accidentally route to a read-only replica.
- **Sharding and partitioning:** distinguish sharding across nodes from partitioning within a database. Require measured scale or operational need; document shard/partition keys, routing, rebalancing, skew, pruning, uniqueness constraints, and cross-partition query/transaction costs.
- **Replication and leader election:** identify the authoritative writer, replication mode/lag, quorum or election behavior, split-brain protection, failover time, and what happens to in-flight writes.
- **CAP theorem and consistency:** state the failure tradeoff for the actual datastore and operation. Do not describe the CAP theorem as a blanket database ranking. Document whether the system uses strong, read-your-writes, or eventual consistency, which reads may be stale, and which operations require strong consistency.
- **Database migrations and schema versioning:** use versioned, repeatable migrations; review destructive changes; prefer expand/migrate/contract for rolling releases; handle backfills, lock duration, compatibility between old/new app versions, and rollback limits. Do not assume a down-migration can restore deleted data.

## 2. Concurrency, locking, memory, and workers

- **Optimistic locking:** where concurrent edits are possible, use version columns/ETags or conditional writes and handle conflicts clearly.
- **Pessimistic locking:** use row or advisory locks only when warranted; keep transactions short and acquire locks in a consistent order.
- **Distributed locks:** define owner, lease/TTL, renewal, fencing or stale-owner protection, crash recovery, and lock-loss behavior. Prefer database constraints/transactions or idempotency if they solve the problem more simply.
- **Race conditions:** test simultaneous requests for balances, inventory, uniqueness, signup, payment, job scheduling, and other read-modify-write operations. Enforce invariants in the database or atomic operation, not only in client logic.
- **Deadlocks:** inspect database deadlock reports and lock ordering; use bounded retries only for recognized retryable transaction failures, and ensure the retried operation is safe.
- **Memory leaks and garbage collection:** inspect heap/RSS over time, retained objects, listeners, timers, caches, buffers, and unbounded collections. Understand GC pauses/pressure for the runtime; do not treat forced GC as a default fix.
- **Thread safety:** identify shared mutable state and runtime concurrency assumptions. Protect critical sections or use immutable/thread-safe primitives where needed.
- **Backpressure:** bound queues, concurrency, request bodies, streams, and producer rates. When downstream systems slow, reject, shed, pause, or defer work intentionally instead of accumulating unbounded memory.
- **Background queues and dead-letter queues (Dead Letter Queues / DLQs):** define retry limits, exponential backoff/jitter, visibility/lease timeout, idempotency, poison-message handling, dead-letter retention, redrive controls, alerting, and operator inspection. A DLQ is not a substitute for fixing repeated failures.
- **Cron jobs and scheduled work:** set timezone and daylight-saving behavior intentionally; prevent overlapping runs where unsafe; make jobs idempotent; track missed/late runs; use distributed coordination when multiple instances can schedule the same task.

## 3. Realtime and service communication

- **WebSockets:** verify authentication at connection time and authorization for every subscription/message; bound connections and message sizes/rates; handle heartbeats, disconnects, reconnect jitter, stale sessions, and multi-instance fanout/pub-sub.
- **Long polling:** use bounded request timeouts, cancellation, client retry backoff, and connection/resource limits. Ensure a request does not hold expensive resources indefinitely.
- **Server-Sent Events (SSE):** verify streaming proxy behavior, heartbeat/keepalive, reconnect and Last-Event-ID semantics, authorization, buffering, and per-client limits. Prefer SSE for one-way server-to-client updates when appropriate; WebSockets are for genuinely bidirectional needs.
- **Webhooks:** validate signatures and timestamps, reject replay, make handlers idempotent, bound payloads, acknowledge promptly when work is queued, and retry safely. Record delivery outcomes without logging secrets.
- **HTTP/2 and HTTP/3:** verify actual edge/origin support and compatibility before claiming use. Check connection multiplexing, proxy/CDN behavior, and performance with representative workloads.
- **gRPC:** when used, verify schema compatibility, deadlines, cancellation, authentication/authorization, status handling, retry policy, streaming limits, and observability.
- **TCP vs UDP:** choose based on application semantics and protocol requirements, not as a generic speed contest. Verify reliability, ordering, congestion handling, and security for the chosen protocol.

## 4. Scaling, caching, and runtime limits

- **Autoscaling:** scale on signals tied to the bottleneck (CPU, concurrency, queue lag, latency, or custom metrics); configure min/max capacity, cooldowns, startup time, and quota limits. Prevent oscillation and runaway scale-out cost.
- **Horizontal scaling vs vertical scaling:** document the current bottleneck and tradeoffs. Horizontal scaling requires statelessness or deliberate shared-state/session handling; vertical scaling has machine/resource ceilings.
- **CDN and edge caching:** cache only responses safe for the audience and freshness policy. Verify origin protection, cache keys, query-string behavior, invalidation, stale serving, and private/authenticated response isolation.
- **Cache invalidation:** define who invalidates, when, and how stale data is tolerated. Test update/delete paths, cache stampedes, cache outage, tenant/user isolation, and any write-behind durability risk.
- **Feature flags:** use server-side authorization for protected features; define owners, defaults, targeting, expiration/removal, audit history, and behavior when the flag provider is unavailable. A flag is not an access-control system.
- **Cold starts and serverless limits:** measure cold and warm latency; verify execution duration, payload size, memory, concurrency, connection reuse, ephemeral storage, and provider quota limits. Avoid architecture claims based only on a warm local run.
- **Latency, throughput, p99 latency, and tail latency:** measure under representative load and include p95/p99 or other tail percentiles, timeouts, errors, queue delay, and resource saturation. Averages can hide tail latency; distinguish service time from end-to-end latency.
- **Network partitions and clock skew:** define timeout and consistency behavior when nodes cannot communicate. Do not assume synchronized clocks for correctness; use monotonic clocks for elapsed time and robust timestamp/idempotency designs for distributed events.
- **DNS:** verify production records, TTL expectations, certificate/hostname coverage, intended redirects, and safe changes. DNS propagation is not instantaneous and DNS is not an access-control boundary.

## 5. Deployments and infrastructure changes

- **Infrastructure as Code (IaC):** version infrastructure definitions, review plans/diffs, separate environments, protect state and secrets, and detect configuration drift. Avoid unmanaged production changes.
- **Terraform:** check state locking/protection, remote state access, secret exposure in state, provider/version pinning, plan review, and drift. Never paste state containing secrets into logs or issues.
- **Helm charts/Kubernetes:** validate rendered manifests, values per environment, resource requests/limits, probes, service accounts/RBAC, secrets, rollout strategy, and chart/version compatibility. Do not require Kubernetes for projects that do not use it.
- **Health checks, liveness probes, and readiness probes:** distinguish liveness (process can continue) from readiness (safe to receive traffic); avoid liveness checks that restart an app merely because a transient dependency is slow. Set probe timeouts and startup behavior deliberately.
- **Feature-flagged releases:** use flags to separate deployment from exposure where useful; ensure safe defaults, staged enablement, telemetry, and a removal plan.
- **Blue-green deployments:** verify traffic switch, compatibility of shared database/state, smoke tests, session behavior, and ability to return traffic safely.
- **Canary releases:** define a small cohort, guardrail metrics, automatic/manual promotion criteria, and abort thresholds. Ensure canary metrics are comparable and sufficient to detect harm.
- **Rolling deployments:** confirm old and new instances can coexist, readiness gates work, capacity remains sufficient during rollout, and background jobs/schemas remain compatible.
- **Rollbacks:** document the trigger, owner, commands, data/schema compatibility, and verification. Code rollback may not reverse migrations or external side effects.
- **Build caching and dependency hell:** use reproducible lockfiles and deterministic build inputs; scope cache keys to relevant inputs; avoid stale artifacts across branches/environments; diagnose conflicting transitive versions and supply-chain risk rather than randomly upgrading everything.

## 6. Security, observability, and production response

- **Secrets management:** use a managed secret store or deployment secret mechanism where available, least privilege, rotation, audit logs, and separation between environments. Never commit secrets or print them in build/runtime logs.
- **IAM:** apply least privilege to people, services, CI, databases, storage, queues, and cloud resources; review wildcard permissions, stale identities, and privilege escalation paths.
- **OAuth and JWT rotation:** validate issuer, audience, expiry, signature, algorithm, state/nonce as relevant; define key rotation and overlap, token revocation/session invalidation, and behavior when discovery/JWKS endpoints fail.
- **TLS, encryption at rest, and encryption in transit:** require TLS for production transport where appropriate; verify certificate renewal and hostname coverage; use provider encryption at rest and deliberate key/secret access. Encryption configuration alone does not prove backups or logs are protected.
- **WAF and DDoS protection:** verify provider-side configuration, rules, rate limits, origin shielding, and bypass paths when warranted. A WAF does not replace application authorization or input handling.
- **CORS and CSRF:** allow only intended origins and methods for credentialed APIs; protect cookie-authenticated state-changing requests with a suitable CSRF strategy. CORS is not authentication.
- **SQL injection, XSS, and SSRF:** use parameterized queries, context-appropriate output encoding/sanitization, and strict outbound destination/redirect controls. For SSRF, block unsafe internal/metadata destinations and re-check DNS/redirect behavior.
- **Encryption at rest/in transit:** identify which data stores, backups, logs, queues, and service links contain sensitive data and verify the actual provider/configuration rather than assuming all paths inherit encryption.
- **Monitoring, logging, metrics, tracing, and alerts:** correlate request/trace IDs across services; capture useful RED/USE-style metrics where applicable (rate, errors, duration, resource saturation); redact secrets/PII; alert on actionable symptoms with an owner/runbook. Logs alone are not observability.
- **SLIs, SLOs, and error budgets:** define user-relevant indicators and targets, measurement windows, burn-rate alerts, and release response when budgets are consumed. Do not copy arbitrary 99.9% targets without product needs.
- **Distributed tracing:** verify trace context propagation across HTTP, queues, and jobs; sampling, cardinality, retention, and sensitive attribute handling. Confirm traces are actually emitted and searchable.
- **Health and alert quality:** test alert routing, deduplication, severity, escalation, and recovery; avoid noisy alerts with no owner or action.
- **Production incidents and on-call:** define ownership, severity, incident roles, escalation, customer communication, mitigation, and follow-up. Verify contact paths and runbooks are usable during an outage.
- **Postmortems:** record impact/timeline, contributing factors, detection gaps, what worked, and owned/time-bound corrective actions. Focus on systemic improvements rather than blame.
- **Chaos engineering:** perform controlled fault injection only with authorization, blast-radius limits, rollback/stop conditions, and monitoring. Start in staging or a small safe scope; do not casually disrupt production.
- **Backups, disaster recovery, and failover:** define RPO/RTO, backup frequency/retention/immutability, restore procedure, dependency order, and failover/failback. Prove restoration with tests; a successful backup job alone is not proof.
- **Multi-region deployment:** justify it with availability/latency requirements and operational capacity. Verify data residency, replication lag, split-brain prevention, regional dependencies, DNS/traffic failover, secret/config parity, and recovery drills.
- **Cost optimization:** measure cost per request/user/workflow, idle resources, egress, logs, replicas, cache hit rate, background work, and provider/model spend. Set budget alerts and hard limits where supported; do not sacrifice correctness or security for nominal savings.

## 7. Versioning and production maintenance

- **API versioning:** identify breaking changes, compatibility windows, deprecation policy, generated-client/schema changes, and monitoring of old versions. Prefer additive changes when feasible and do not silently break deployed clients.
- **Semantic versioning:** use MAJOR for incompatible public API changes, MINOR for backward-compatible functionality, and PATCH for backward-compatible fixes when semver is the chosen contract. Document exceptions and pre-release rules.
- **Dependency management:** lock versions, inspect transitive conflicts, patch known vulnerabilities, remove unused packages safely, and test upgrades. Do not let a lockfile or version number stand in for vulnerability review.
- **Operational runbooks:** document common deploy, rollback, queue redrive, restore, failover, secret rotation, and incident actions. Keep instructions current and test them periodically.

## 8. Verification rules

For each applicable item, report **PASS**, **FAIL**, **UNKNOWN**, or **NOT APPLICABLE** with evidence and next action. For provider-managed controls, ask for the dashboard, configuration, test output, or runbook evidence. Do not claim production behavior from source code alone.

Do not run destructive migrations, failovers, chaos experiments, load tests against production, or infrastructure changes without explicit authorization and a controlled plan. Prefer read-only inspection first. State the limits of any audit and do not call a checklist a guarantee of reliability.
