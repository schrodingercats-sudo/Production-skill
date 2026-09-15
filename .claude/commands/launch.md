# Production Pup: Launch

Run the final pre-launch Production Pup gate.

Read `SKILL.md` first and use its Final Pre-Launch Gate, Security Verification Matrix, and audit-reporting rules as the source of truth.

## Command

`/launch`

Perform a complete release-readiness check covering:

- core functionality
- authentication, authorization, object permissions, tenant isolation, and admin routes
- secrets, environment files, Git history, and production artifacts
- input validation, SQL/NoSQL injection, XSS, CSRF, SSRF, path traversal, command injection, unsafe deserialization, and mass assignment where relevant
- sessions, cookies, JWT validation, OAuth/OIDC, password reset, and webhook verification where relevant
- payment and entitlement checks on the server
- rate limits, abuse controls, AI spend controls, and default credentials
- staging/test environment isolation and production debug leakage
- dependency vulnerabilities, package supply-chain risk, and abandoned dependencies
- prompt injection and AI tool permission boundaries where AI exists
- audit logs, security monitoring, alerts, backups, restore testing, and internal dashboards where required
- HTTPS/TLS, CORS, security headers, and secure cookies
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

For security findings, use PASS, FAIL, UNKNOWN, or NOT APPLICABLE and cite evidence. Do not treat UNKNOWN as PASS. Do not declare the project ready if critical items are outstanding or unverifiable. Produce a concise release report with blockers, evidence, and recommended next actions.

Arguments: $ARGUMENTS
