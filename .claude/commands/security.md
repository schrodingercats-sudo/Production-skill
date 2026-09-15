# Production Pup: Security

Run the security-focused Production Pup audit.

Read `SKILL.md` first and use its Security Audit as the source of truth.

## Command

`/security`

Audit and, when requested, fix:

- exposed secrets and environment variables
- leaked keys in source or Git history
- authentication and authorization
- admin-route protection
- object-level permissions / IDOR / BOLA
- XSS and unsafe HTML
- SQL injection and query safety
- database permissions
- rate limits and abuse controls
- spending limits for expensive APIs or AI endpoints
- secure file uploads
- CSRF
- CORS
- HTTPS and mixed content
- security headers
- secure cookies and sessions
- debug mode and production leakage

Do not claim a system is secure merely because code looks correct. Verify what can actually be tested and report remaining uncertainty.

Arguments: $ARGUMENTS
