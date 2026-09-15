<p align="center">
  <img src="./assets/production-pup-banner.png" alt="Production Pup Skill" width="100%">
</p>

<p align="center">
  <strong>A production-minded quality gate for websites and web apps.</strong>
</p>

<p align="center">
  Build with intention. Check the details. Ship with confidence.
</p>

<p align="center">
  <a href="./SKILL.md">Skill File</a>
  ·
  <a href="#what-it-checks">What It Checks</a>
  ·
  <a href="#slash-commands">Slash Commands</a>
  ·
  <a href="#how-to-use">How to Use</a>
</p>

---

## 🐶 What is Production Pup?

**Production Pup** is a reusable skill for AI coding agents and developers who want to take a website or web app beyond "it works."

It acts as a **pre-launch quality gate** covering security, privacy, SEO, accessibility, performance, responsive behavior, production cleanup, trustworthy content, and intentional design.

> **Don't ship a demo when you meant to ship a product.**

The skill is deliberately skeptical. It does not treat a checklist as proof that something is secure or production-ready. Requirements should be implemented, verified, delegated to a trusted framework/provider, marked not applicable, or clearly left outstanding.

## ✦ What It Checks

| Area | What Production Pup looks for |
| --- | --- |
| **Product understanding** | Goals, users, routes, data, integrations, auth, privacy, and product-specific requirements before implementation. |
| **Design quality** | Intentional visual systems, typography, spacing, color, motion, hierarchy, and protection against generic AI/vibe-coded UI. |
| **Security** | Evidence-driven 54-check coverage across secrets, auth, authorization, injection, sessions, APIs, payments, files, AI tools, dependencies, infrastructure, logging, backups, and browser security. |
| **Privacy** | Privacy policies, terms, cookies, consent, analytics, tracking, third-party embeds, and data minimization. |
| **SEO** | Titles, descriptions, headings, canonicals, sitemap, robots, structured data, social previews, favicon, 404 pages, and broken links. |
| **Performance** | Image optimization, bundle size, loading states, API latency, layout stability, caching, database queries, pagination, and production-build performance. |
| **Responsive UX** | Mobile layouts, navigation, forms, tables, dialogs, touch targets, overflow, and fixed elements. |
| **Accessibility** | Keyboard navigation, focus states, contrast, semantic HTML, labels, alt text, motion, controls, and useful errors. |
| **Forms** | Client and server validation, invalid input, duplicate submissions, failures, mobile input, and spam/abuse cases. |
| **Trust** | No fabricated testimonials, metrics, customer logos, certifications, capabilities, business details, or unsupported claims. |
| **Production cleanup** | Console errors, network failures, starter artifacts, debug mode, source maps, dependencies, configuration, and deployment readiness. |
| **Final verification** | A clear distinction between implemented, verified, provider-handled, not applicable, and outstanding requirements. |

## 🔐 Evidence-Driven Security

The security layer now includes the supplied Part 3 launch filter as a cumulative **54-check verification matrix**. The key rule is simple: if you cannot point to the code, setting, configuration, test, or log that proves a guardrail exists, do not mark it PASS.

Security checks cover four groups:

- **Secrets, auth, authorization, and input**: credentials, `.env`, hardcoded secrets, authentication, server-side permissions, cross-user access, database rules, admin routes, debug tooling, logs, Git history, frontend exposure, validation, SQL injection, and NoSQL injection.
- **Web, sessions, APIs, files, and payments**: XSS, CSRF, uploads, path traversal, SSRF, password reset, sessions, JWTs, CORS, rate limits, staging, default credentials, webhooks, payments, IDOR/BOLA, user-controlled roles/IDs, logs, and source maps.
- **Dependencies, AI, data, and infrastructure**: vulnerable or malicious packages, prompt injection, AI tool authorization, least-privilege databases, audit logs, monitoring, backups, internal dashboards, security headers, cookies, encryption, tenant isolation, AI-generated code review, mass assignment, OS command injection, deserialization, and OAuth/OIDC.
- **Verification discipline**: every relevant finding is classified as PASS, FAIL, UNKNOWN, or NOT APPLICABLE, with evidence and a verification path.

This is an audit framework, not a penetration test or a guarantee that an application cannot be compromised.

## 🧭 How It Thinks

```text
Understand
    ↓
Inspect
    ↓
Build the foundation
    ↓
Apply intentional design
    ↓
Security pass
    ↓
Privacy pass
    ↓
SEO + accessibility pass
    ↓
Performance pass
    ↓
Production pass
    ↓
Trust pass
    ↓
Final visual audit
    ↓
Verify what is actually ready
```

A polished interface cannot compensate for broken authorization, leaked API keys, missing error states, or fake claims.

## ⚡ Slash Commands

Production Pup includes **user-invocable slash commands** for focused workflows. The commands use the main `SKILL.md` as their source of truth.

| Command | Purpose |
| --- | --- |
| `/production-pup` | Run the complete Production Pup audit. |
| `/fix` | Audit, implement relevant fixes, then verify them. |
| `/report` | Audit only and produce a structured readiness report. No project changes. |
| `/security` | Run the evidence-driven security audit, including the 54-check matrix. |
| `/seo` | Focus on SEO, metadata, crawling, structured data, social previews, and discoverability. |
| `/performance` | Focus on frontend, API, database, caching, bundles, queries, and scalability. |
| `/design` | Focus on visual quality, design systems, UX polish, and anti-vibecoding patterns. |
| `/accessibility` | Focus on keyboard, semantic HTML, contrast, labels, motion, and accessible interaction. |
| `/launch` | Run the final release-readiness gate and identify blockers before shipping. |

### Example

```text
/production-pup
```

Runs the complete audit.

```text
/security
```

Runs the evidence-driven security workflow.

```text
/fix
```

Audits, fixes relevant issues, and verifies the changes.

```text
/report
```

Creates a report without modifying the project.

## 🛠️ How to Use

The main skill lives in `SKILL.md`. Focused slash-command workflows live directly under `.claude/commands/`.

Give the skill to your AI coding agent or use the slash commands when your agent supports repository command files.

### For an AI coding agent

Use the skill when asking an agent to:

- build a new website or web app
- finish an existing project
- audit a project before deployment
- review production readiness
- improve security and privacy
- fix accessibility or responsive issues
- clean up a generated/vibe-coded interface

The preferred workflow is to invoke the relevant Production Pup command rather than manually pasting a long prompt.

## 🔍 The Production Standard

Production Pup does **not** say "production-ready" just because the page renders.

Before making that claim, the project should have:

- working core functionality
- protected secrets
- server-side authorization
- validated user input
- appropriate abuse protection
- privacy/legal pages where required
- intentional analytics and tracking
- useful SEO metadata on public pages
- accessible interactions
- responsive layouts
- loading, empty, success, and error states
- optimized assets and reasonable performance
- a clean production build
- no unexplained critical console or network errors
- no fake credibility or unsupported claims
- a coherent, product-specific visual system
- applicable security checks verified with evidence

If something cannot be verified, **say so instead of pretending it is done.**

## 🎨 Design Philosophy

Production Pup favors **intentional design over trend stacking**.

Gradients, glassmorphism, giant shadows, generic bento grids, decorative code windows, excessive animation, and other fashionable patterns are not automatically forbidden. They simply need a reason to exist.

> **Every major visual choice should earn its place.**

## 📋 Quick Pre-Launch Check

- [ ] Privacy Policy exists if required
- [ ] Terms exist if required
- [ ] No frontend secrets
- [ ] HTTPS is configured
- [ ] Server-side auth and object permissions are verified
- [ ] Security findings are evidence-backed
- [ ] Page titles and descriptions are correct
- [ ] Social preview is configured
- [ ] Favicon is present
- [ ] Sitemap and robots configuration are correct
- [ ] Images are optimized
- [ ] Performance has been checked
- [ ] Contrast has been checked
- [ ] Mobile layout works
- [ ] Tracking and cookie behavior is intentional
- [ ] Custom 404 exists
- [ ] Broken links are fixed
- [ ] Forms validate correctly
- [ ] Spam protection exists where needed
- [ ] Keyboard navigation works
- [ ] Claims and business details are real
- [ ] Production build has been tested

For the full audit, use the [complete skill file](./SKILL.md).

## 📁 Repository Structure

```text
Production-skill/
├── README.md
├── SKILL.md
├── production_ready_website_app_skill_merged.md
├── .claude/
│   └── commands/
│       ├── production-pup.md
│       ├── fix.md
│       ├── report.md
│       ├── security.md
│       ├── seo.md
│       ├── performance.md
│       ├── design.md
│       ├── accessibility.md
│       └── launch.md
└── assets/
    └── production-pup-banner.png
```

The banner artwork is intentionally kept separate from the skill itself so the documentation stays portable.

## 🐾 Philosophy

**Accuracy beats confidence.**  
**Verification beats assumption.**  
**Real product behavior beats decorative mockups.**  
**Intentional design beats trend stacking.**

**If you cannot verify it, don't call it production-ready.**

---

## Star History

<a href="https://www.star-history.com/?repos=schrodingercats-sudo%2Fproduction-skill&type=timeline&legend=bottom-right">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/chart?repos=schrodingercats-sudo/production-skill&type=date&theme=dark&legend=bottom-right" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/chart?repos=schrodingercats-sudo/production-skill&type=date&legend=bottom-right" />
   <img alt="Star History Chart" src="https://api.star-history.com/chart?repos=schrodingercats-sudo/production-skill&type=date&legend=bottom-right" />
 </picture>
</a>

---

<p align="center">Made for builders who want the last 10% to actually matter. 🐾</p>
