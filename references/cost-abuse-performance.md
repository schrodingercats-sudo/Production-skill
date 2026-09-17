# Cost, Abuse & Resource Protection Reference

Use this reference for AI apps, API-heavy products, file-serving apps, SaaS products, and any project where an attacker or accidental failure can create infrastructure, model, bandwidth, or database costs.

The supplied videos highlight five concrete failure patterns: missing spend caps, whole-database reads, retry loops, unrestricted bot downloads, and missing rate limits.

## 1. Spend limits

Audit:

- provider or application spend caps where the service supports them
- budget alerts for AI/model, email, storage, database, hosting, and other metered services
- automatic pause or hard caps where appropriate and supported
- per-user, per-tenant, or per-IP usage ceilings for expensive operations
- whether alerts merely notify an operator or actually prevent additional spend

An email alert is not the same thing as a hard usage cap. Report the distinction clearly.

## 2. Whole-database reads

Look for endpoints that return far more records or columns than the UI actually needs.

Check:

- `SELECT *` or equivalent over-fetching
- fetching an entire table and slicing it in application code
- missing pagination
- missing server-side filters
- endpoints that expose every row when the page only displays a small subset
- returning unnecessary sensitive fields

Prefer server-side filtering, projection, pagination, and authorization. Do not add arbitrary limits that break legitimate product behavior.

## 3. Retry loops

Audit retries around APIs, queues, webhooks, model calls, and database operations.

Check for:

- retries without a maximum attempt count
- immediate tight-loop retries
- retrying non-idempotent operations
- multiple layers each retrying the same request
- retries that multiply expensive model/API calls
- missing exponential backoff and jitter where repeated retries are appropriate
- missing idempotency keys for operations that may be repeated

A failed request should not be capable of turning into an uncontrolled request storm or unexpected bill.

## 4. Rate limits

Rate-limit expensive or abuse-prone operations server-side.

Prioritize:

- AI/model generation
- authentication
- password reset
- signup
- uploads
- email/SMS sending
- search and scraping-heavy endpoints
- payment or credit operations
- public APIs
- file downloads

Check limits by the appropriate identity signal, such as user, tenant, IP, API key, or route, rather than relying on a single easily-bypassed client-side counter.

## 5. Bot downloads and bandwidth abuse

For public or semi-public files:

- check whether the same file can be downloaded indefinitely without controls
- consider signed/expiring URLs for private files
- enforce authorization before issuing private download URLs
- apply sensible rate or quota limits to expensive downloads
- use CDN controls where appropriate
- monitor unusual bandwidth spikes
- prevent a download endpoint from becoming an unbounded cost center

Do not require authentication for genuinely public assets merely because a rate limit exists; choose controls based on the asset and threat model.

## 6. Resource limits

Across the application, look for explicit ceilings on:

- request body size
- upload size and count
- execution timeouts
- query complexity/depth
- pagination size
- queue retries
- concurrency
- storage
- model tokens or generations
- email/SMS sends
- background jobs
- download bandwidth

## Verification

For each finding, explain:

1. What operation can be abused.
2. Whether the cost/resource impact is bounded.
3. Which server-side control enforces the bound.
4. How the limit behaves when reached.
5. How to test the limit safely without generating unnecessary real-world cost.

Do not claim a fixed dollar exposure unless the project provides enough provider pricing and usage data to support the calculation.
