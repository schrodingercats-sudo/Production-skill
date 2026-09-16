# Production Pup: Report

Run a Production Pup audit without making project changes and produce a structured report.

Read `SKILL.md` first and use its audit-reporting rules as the source of truth.

Also read:
- `references/privacy-legal-readiness.md`
- `references/trust-conversion-seo.md`
- `references/security-operational-hardening.md`
- `references/design-quality.md`

## Command

`/report`

Return:

1. Executive readiness summary
2. Critical blockers
3. High-priority issues
4. Medium/low-priority issues
5. Verified strengths
6. Provider-handled / ASK ME items requiring external evidence
7. Not-applicable items
8. UNKNOWN/outstanding items that could not be verified
9. Recommended next actions

Include relevant findings from privacy/legal readiness, trust/conversion, local SEO, operational security, and UI interaction quality. Do not treat provider settings or legal applicability as proven by repository source code. Do not fabricate evidence, claims, business details, or compliance status.

Classify findings as Implemented, Verified, Provider handled, Not applicable, UNKNOWN/Needs evidence, or Outstanding. Do not modify files in report-only mode.

Arguments: $ARGUMENTS
