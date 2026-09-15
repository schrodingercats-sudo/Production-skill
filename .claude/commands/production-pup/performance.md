# Production Pup: Performance

Run the performance and scalability-focused Production Pup audit.

Read `SKILL.md` first and use its Performance and Scalability Audit as the source of truth.

## Command

`/production-pup/performance`

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
- over-fetching
- debouncing
- pagination
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

Identify the bottleneck before optimizing. Do not add infrastructure or caching merely because it is fashionable.
