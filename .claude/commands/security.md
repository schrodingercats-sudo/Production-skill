# Production Pup: Security

Run the security-focused Production Pup audit.

Read `SKILL.md` first and use its Security Audit and 70-check Security Verification Matrix as the source of truth.

Also read `references/security-operational-hardening.md` for controls that require deployment, provider, DNS, registrar, billing, backup, or independent-review evidence.

## Command

`/security`

### Audit method

For every relevant check, return exactly one of:

- **PASS**: evidence proves the guardrail exists and works as expected.
- **FAIL**: evidence shows the guardrail is missing or broken.
- **UNKNOWN**: the guardrail may exist, but available code, configuration, tests, or logs do not prove it.
- **NOT APPLICABLE**: the project genuinely does not use the affected feature or risk.
- **ASK ME**: the supplied security reference says the control must be verified outside the repository, so ask the operator for evidence instead of scoring source code.

For every PASS, cite the exact file, configuration, setting, test, or log that proves it. Do not mark PASS from visual inspection alone when runtime or provider evidence is required. For FAIL or UNKNOWN, give the realistic failure mode, smallest safe fix, and verification step.

Do not change production data or infrastructure during an audit. Prioritize authentication, authorization, private data, payments, admin access, secrets, AI tools, and spend.

### Security coverage

Audit and, when requested, fix:

- database credentials, `.env` files, hardcoded secrets, frontend-secret exposure, and secrets in Git history
- authentication, MFA for privileged accounts, server-side authorization, admin routes, object-level authorization, IDOR/BOLA, tenant isolation, and user-controlled roles or IDs
- account enumeration, password reset flows, sessions, JWT validation, cookies, OAuth/OIDC/social login, and CSRF
- input validation, SQL injection, NoSQL injection, XSS, mass assignment, command/OS injection, unsafe deserialization, and business-logic abuse
- race conditions, duplicate processing, webhook replay, webhook signatures, and server-side payment/entitlement checks
- file upload controls, path traversal, SSRF, and unsafe file access
- CORS, HTTPS/TLS, mixed content, security headers, browser protections, and open redirects
- rate limits, abuse controls, resource limits, AI/model endpoints, spend controls, and default credentials
- staging/test environments, debug tools, build logs, verbose errors, sensitive logs, source maps, and public internal dashboards
- dependency vulnerabilities, abandoned packages, malicious packages, lockfiles, pinned CI actions, and software supply-chain risk
- prompt injection, AI sensitive-information disclosure, unsafe AI output handling, and AI tool authorization
- excessive AI agent agency and confirmation boundaries for consequential actions
- audit logging, security monitoring, alerting, backup/restore testing, and incident-relevant observability
- least-privilege database access and sensitive data protection in transit and at rest
- CI/CD credentials, deployment environment protection, third-party build actions/scripts, and fail-closed security behavior
- sensitive browser storage such as localStorage, IndexedDB, and caches
- GraphQL, WebSocket, and realtime endpoint authentication, authorization, and abuse limits
- review of AI-generated code before shipping, especially auth, payments, data, and permission logic
- `SECURITY DEFINER` functions and other helpers that could bypass row-level security
- authenticated/private response caching and CDN `Cache-Control` behavior
- DNS record integrity and dangling-record risk when DNS configuration is available
- third-party script integrity and Subresource Integrity where supported
- public resource identifiers and avoidable sequential-ID enumeration
- log redaction for tokens, passwords, card data, and other sensitive values

### Operational / provider checks

Read `references/security-operational-hardening.md` and separate repository evidence from operator/provider evidence. Ask for evidence of backups and restore tests, billing/spend alerts, registrar/DNS 2FA and transfer lock, CAA records, dangling DNS, WAF, restricted admin access, canary detection, and recent independent security review or penetration testing. Do not infer these controls from application source code.

### Evidence standard

The governing rule is: if you cannot point to the code, setting, configuration, test, or log that proves a guardrail exists, treat it as missing or UNKNOWN rather than assuming it is present. If the control is explicitly external to the repository, use ASK ME and state the evidence required.

After fixes, re-test the deployed path where applicable and re-run the audit after meaningful changes to authentication, data, infrastructure, dependencies, payments, or AI tools.

Do not claim a system is secure merely because code looks correct. This is an audit workflow, not a penetration test or guarantee.

Arguments: $ARGUMENTS
