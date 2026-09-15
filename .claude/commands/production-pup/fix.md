# Production Pup: Fix

Run a Production Pup audit and then fix the relevant issues found in the project.

Read `SKILL.md` first and treat it as the source of truth.

## Command

`/production-pup/fix`

Workflow:

1. Inspect before editing.
2. Audit the project against the Production Pup skill.
3. Prioritize critical security, correctness, privacy, accessibility, and launch blockers first.
4. Implement fixes using the existing stack unless a concrete reason requires otherwise.
5. Re-run relevant tests, builds, static checks, and browser checks.
6. Report what changed, what was verified, and what remains outstanding.

Never hide an unresolved issue just because a fix was attempted.
