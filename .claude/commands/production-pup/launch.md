# Production Pup: Launch

Run the final pre-launch Production Pup gate.

Read `SKILL.md` first and use its Final Pre-Launch Gate and audit-reporting rules as the source of truth.

## Command

`/production-pup/launch`

Perform a complete release-readiness check covering:

- core functionality
- authentication and permissions
- secrets
- input/API protection
- abuse protection
- HTTPS and browser security
- privacy and legal requirements
- SEO basics
- favicon and social metadata
- sitemap and robots configuration
- 404 and error states
- form validation
- accessibility
- mobile layouts
- optimized assets
- loading, empty, success, and error states
- API and database performance
- caching
- database indexes and query patterns
- N+1 queries
- pagination
- CDN/load balancing where appropriate
- connection pooling where needed
- production JavaScript/CSS optimization
- unused dependencies
- deferred non-critical scripts
- console and network errors
- real content and claims
- successful production build

Do not declare the project ready if critical items are outstanding or unverifiable. Produce a concise release report with blockers and recommended next actions.
