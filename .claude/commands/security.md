# Production Pup: Security

Run the security-focused Production Pup audit.

Read `SKILL.md` first and use its Security Audit and 54-check Security Verification Matrix as the source of truth.

## Command

`/security`

### Audit method

For every relevant check, return exactly one of:

- **PASS**: evidence proves the guardrail exists and works as expected.
- **FAIL**: evidence shows the guardrail is missing or broken.
- **UNKNOWN**: the guardrail may exist, but available code, configuration, tests, or logs do not prove it.
- **NOT APPLICABLE**: the project genuinely does not use the affected feature or risk.

For every PASS, cite the exact file, configuration, setting, test, or log that proves it. Do not mark PASS from visual inspection alone when runtime evidence is required. For FAIL or UNKNOWN, give the realistic failure mode, smallest safe fix, and verification step.

Do not change production data or infrastructure during an audit. Prioritize authentication, authorization, private data, payments, admin access, secrets, AI tools, and spend.

### Security coverage

Audit and, when requested, fix:

- database credentials, `.env` files, hardcoded secrets, frontend-secret exposure, and secrets in Git history
- authentication, server-side authorization, admin routes, object-level authorization, IDOR/BOLA, tenant isolation, and user-controlled roles or IDs
- database permissions and least-privilege database roles
- input validation, SQL injection, NoSQL injection, XSS, mass assignment, command/OS injection, and unsafe deserialization
- file upload controls, path traversal, SSRF, and unsafe file access
- password reset flows, sessions, JWT validation, cookies, OAuth/OIDC/social login, and CSRF
- CORS, HTTPS/TLS, mixed content, security headers, and browser protections
- rate limits, abuse controls, AI/model endpoints, spend controls, and default credentials
- staging/test environments, debug tools, build logs, verbose errors, sensitive logs, source maps, and public internal dashboards
- webhook signature verification and server-side payment/entitlement checks
- dependency vulnerabilities, abandoned packages, malicious packages, and software supply-chain risk
- prompt injection and AI tool authorization so model actions cannot bypass real user or tenant permissions
- audit logging, security monitoring, alerting, backup/restore testing, and incident-relevant observability
- sensitive data protection in transit and at rest
- review of AI-generated code before shipping, especially auth, payments, data, and permission logic

### Evidence standard

The governing rule is: if you cannot point to the code, setting, configuration, test, or log that proves a guardrail exists, treat it as missing or UNKNOWN rather than assuming it is present.

After fixes, re-test the deployed path where applicable and re-run the audit after major security changes.

Do not claim a system is secure merely because code looks correct. This is an audit workflow, not a penetration test or guarantee.

Arguments: $ARGUMENTS
