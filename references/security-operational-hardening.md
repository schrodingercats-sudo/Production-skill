# Security Operational Hardening Reference

Use this reference after the repository-level security audit. It covers controls that are often outside application source code or require deployment/provider evidence.

The supplied security reference explicitly separates repository-checkable controls from questions that must be answered by the operator/provider. Do not pretend these are proven by source code alone.

## Operational checks: ASK ME / VERIFY EXTERNALLY

1. Automated backups are running.
2. A restore from backup has actually been tested.
3. Billing and spend alerts are configured for relevant infrastructure, APIs, and paid services.
4. Registrar and DNS accounts use 2FA, and domain transfer lock is enabled where supported.
5. CAA records are configured where appropriate.
6. DNS contains no dangling records that point to decommissioned or unclaimed services.
7. A WAF is deployed when appropriate for the application's threat model and exposure.
8. Admin access is IP-allowlisted or placed behind a VPN/other restricted network boundary where appropriate.
9. Canary tokens or equivalent detection signals are used when they provide meaningful value for the project.
10. A penetration test or independent security review has been completed within the relevant review period.

## Source/configuration checks reinforced by the supplied material

Make these explicit during the repository audit:

- `SECURITY DEFINER` functions cannot bypass intended row-level security or ownership controls.
- Authenticated/private responses use appropriate `Cache-Control` directives so a CDN cannot serve one user's private response to another user.
- DNS records do not point at decommissioned resources when DNS configuration is available to inspect.
- Third-party GitHub Actions are pinned to commit SHAs rather than movable version tags where supply-chain integrity requires it.
- Inbound webhooks verify signatures and reject stale/replayed events.
- External scripts use Subresource Integrity where the script-loading architecture supports it.
- Public resource identifiers do not expose unnecessary sequential database IDs when enumeration would create a privacy or authorization risk.
- Logs redact tokens, passwords, card data, and other sensitive values.

## Evidence rules

For code/configuration checks, cite the exact file, configuration, test, or log.

For provider or operational checks, request evidence such as:

- backup job history and a restore-test record
- billing/alert configuration
- registrar/DNS security settings
- DNS zone records and ownership of target services
- WAF configuration
- VPN/IP allowlist configuration
- canary alert test
- recent independent security review or penetration-test report

If that evidence is unavailable, mark the item UNKNOWN or ASK ME rather than PASS.

This reference does not make a security guarantee and does not replace a professional penetration test or independent security review.
