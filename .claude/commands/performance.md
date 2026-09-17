# Production Pup: Performance

Run the performance and scalability-focused Production Pup audit.

Read `SKILL.md` first and use its Performance and Scalability Audit as the source of truth.

Also read `references/cost-abuse-performance.md` for cost and resource-exhaustion patterns.

## Command

`/performance`

Audit and, when requested, fix:

- image size and compression
- modern image formats
- lazy loading
- JavaScript and CSS bundles
- code splitting
- unused dependencies
- unnecessary client work
- unnecessary component re-renders
- loading and layout stability
- excessive network requests
- API response caching
- expensive query/computation caching
- API payload compression
- over-fetching and whole-database reads
- debouncing
- pagination and unbounded list fetching
- lazy loading of expensive features
- deferred non-critical scripts
- database indexes
- slow queries
- N+1 queries
- repeated database fetches
- database connection pooling
- CDN usage where justified
- load balancing where justified
- cache invalidation
- realistic production-build performance

### Cost and resource exhaustion

Also inspect:

- missing spend caps and budget alerts for metered services
- distinction between alerts and hard caps/automatic pause controls
- expensive AI/model endpoints without usage ceilings
- retry loops, retry multiplication, and retries without maximum attempts
- retries of non-idempotent operations
- missing backoff/jitter where appropriate
- API, download, upload, email, and background-job rate limits
- unrestricted repeated file downloads and bandwidth abuse
- request, upload, timeout, concurrency, queue, storage, token, and usage limits

For every cost-related finding, identify the operation, current bound, enforcement point, and safe verification method. Do not invent dollar exposure without reliable usage and pricing data.

Identify the bottleneck before optimizing. Do not add infrastructure or caching merely because it is fashionable.

Arguments: $ARGUMENTS
