# Production Pup: Launch

Run the final pre-launch Production Pup gate.

Read `SKILL.md` first and use its Final Pre-Launch Gate, 70-check Security Verification Matrix, and audit-reporting rules as the source of truth.

Also apply:
- `references/design-quality.md`
- `references/privacy-legal-readiness.md`
- `references/trust-conversion-seo.md`
- `references/security-operational-hardening.md`

## Command

`/launch`

Perform a complete release-readiness check covering:

- core functionality
- authentication, authorization, privileged-account MFA, and permissions
- secrets and Git history
- input/API protection, business-logic abuse, race conditions, and fail-closed behavior
- rate limits, resource limits, and abuse protection
- AI prompt injection, sensitive-data disclosure, unsafe AI output handling, tool permissions, and agent agency
- webhook signatures, replay/duplicate processing, and server-side payment/entitlement checks
- OAuth/OIDC/social login and account enumeration
- file uploads, path traversal, SSRF, and open redirects
- HTTPS/TLS, cookies, CORS, security headers, and browser storage
- dependencies, lockfiles, CI/CD credentials, build actions, and pinned sensitive actions
- `SECURITY DEFINER` functions, private-response caching, DNS integrity, third-party script integrity, resource-ID enumeration, and sensitive log redaction
- audit logs, monitoring/alerts, backups/restores, and internal dashboards
- provider/operator evidence for backup restore tests, billing/spend alerts, registrar/DNS 2FA and transfer lock, CAA records, dangling DNS, WAF, restricted admin access, canary detection, and independent security review
- GraphQL/WebSocket/realtime security where used
- privacy and legal readiness using `references/privacy-legal-readiness.md`
- actual data collection, consent, cookie/tracking behavior, third-party SDKs, deletion/retention behavior, claims, pricing/fees, licensing, accessibility, and contact details
- SEO basics
- unique page titles and useful meta descriptions
- sensible H1/heading structure and canonical URLs
- sitemap, robots configuration, and `lang` attribution
- favicon and social metadata
- 404 and error states
- broken links and footer links
- trust/conversion details including clear CTAs, short forms, FAQs, service/product pages, real case studies, booking/confirmation flows, visible contact details, and legitimate response-time promises where applicable
- local SEO checks where the project is location-based, without inventing locations or backlinks
- form validation, success messages, error messages, and duplicate-submission handling
- clickable logo/home navigation where appropriate
- clickable phone numbers and email addresses where appropriate
- no placeholder text or unused navigation
- accessibility
- button text/icon contrast in every important state
- overlapping buttons and CTA groups
- pointer-event/hit-target collisions
- responsive flex/grid wrapping and breakpoint collisions
- navigation, modal, dropdown, tooltip, and overlay collisions
- meaningful hover/focus/active/loading/success/error states
- icon consistency and accessible names for icon-only controls
- no emoji UI icons
- no new Lucide/lucide-react UI icons
- purposeful micro-interactions
- reduced-motion behavior
- animation performance and restraint
- mobile layouts, mobile menus, horizontal-overflow checks, and overall mobile optimization
- optimized and appropriately sized images
- loading, empty, success, and error states
- API and database performance
- caching
- database indexes and query patterns
- N+1 queries
- pagination
- CDN/load balancing where appropriate
- connection pooling where needed
- production JavaScript/CSS optimization
- unused dependencies and assets
- deferred non-critical scripts
- console and network errors
- real content and claims
- successful production build

Do not declare the project ready if critical items are outstanding or unverifiable. Produce a concise release report with evidence, blockers, UNKNOWN/provider-evidence items, and recommended next actions.

Arguments: $ARGUMENTS
