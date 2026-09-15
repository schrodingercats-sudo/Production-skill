# Production Pup

Run the complete Production Pup quality gate.

Read and follow the repository's `SKILL.md` as the source of truth for the audit.

## Command

`/production-pup`

## Behavior

1. Inspect the existing project before changing anything.
2. Determine the product, users, routes, data, integrations, auth, privacy requirements, and deployment context.
3. Run the full Production Pup audit across design, security, privacy, SEO, performance, responsive UX, accessibility, forms, trust, and production cleanup.
4. Implement relevant fixes when the user has asked for an audit-and-fix workflow. Do not blindly rewrite the stack.
5. Verify changes with appropriate tests, builds, browser checks, or static inspection.
6. Report results as Implemented, Verified, Provider handled, Not applicable, or Outstanding.

If arguments are supplied, treat them as additional project context or priorities, but still follow the full skill unless a more specific Production Pup command was used.

Arguments: $ARGUMENTS
