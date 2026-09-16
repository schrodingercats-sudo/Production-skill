# Production Pup

Run the complete Production Pup quality gate.

Read and follow the repository's `SKILL.md` as the source of truth for the audit.

Also read:
- `references/design-quality.md`
- `references/privacy-legal-readiness.md`
- `references/trust-conversion-seo.md`
- `references/security-operational-hardening.md`

Apply these references where relevant. External/provider controls must be verified separately rather than inferred from source code.

## Command

`/production-pup`

## Behavior

1. Inspect the existing project before changing anything.
2. Determine the product, users, routes, data, integrations, auth, privacy requirements, and deployment context.
3. Run the full Production Pup audit across design, security, privacy/legal readiness, SEO, performance, responsive UX, accessibility, forms, trust, conversion, interaction polish, and production cleanup.
4. Implement relevant fixes when the user has asked for an audit-and-fix workflow. Do not blindly rewrite the stack.
5. Verify changes with appropriate tests, builds, browser checks, or static inspection.
6. For interactive UI, verify actual hit areas and interaction states, not only screenshots. Check button contrast, button overlap/collision, hover/focus/active states, responsive wrapping, icon consistency, and meaningful micro-interactions.
7. For React projects, consider Motion for purposeful micro-interactions and layout transitions where appropriate. Do not add animation merely for decoration or stack animation libraries without a concrete reason.
8. Do not use emoji as UI icons or introduce Lucide/lucide-react for new UI icons. Prefer a deliberate icon family or project-specific SVG system.
9. Audit privacy/legal readiness without pretending that a generic policy proves compliance. Verify actual data collection, consent, SDKs, deletion behavior, claims, pricing, accessibility, licensing, and contact details where applicable.
10. Audit trust and conversion details such as real CTAs, short forms, booking/confirmation flows, useful FAQs, internal links, service pages, real case studies, and visible contact information. Never invent trust signals or claims.
11. Audit local SEO only when the project is location-based. Do not invent locations, keyword-stuff, or fake backlinks.
12. Separate repository-verifiable security controls from provider/operator controls such as backups, restore tests, billing alerts, registrar/DNS security, WAF, restricted admin access, and independent security review.
13. Report results as Implemented, Verified, Provider handled, Not applicable, UNKNOWN/Needs evidence, or Outstanding.

If arguments are supplied, treat them as additional project context or priorities, but still follow the full skill unless a more specific Production Pup command was used.

Arguments: $ARGUMENTS
