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

It acts as a **pre-launch quality gate** covering security, privacy/legal readiness, SEO, accessibility, performance, responsive behavior, production cleanup, trustworthy content, conversion details, and intentional design.

> **Don't ship a demo when you meant to ship a product.**

The skill is deliberately skeptical. It does not treat a checklist as proof that something is secure or production-ready. Requirements should be implemented, verified, delegated to a trusted framework/provider, marked not applicable, or clearly left outstanding.

## ✦ What It Checks

| Area | What Production Pup looks for |
| --- | --- |
| **Product understanding** | Goals, users, routes, data, integrations, auth, privacy, and product-specific requirements before implementation. |
| **Design quality** | Intentional visual systems, typography, spacing, color, motion, hierarchy, button correctness, collision-free layouts, and protection against generic AI/vibe-coded UI. |
| **Security** | Evidence-driven **70-check** coverage across secrets, auth, MFA, authorization, injection, business logic, race conditions, sessions, APIs, payments, files, AI security, CI/CD, browser security, redirects, realtime endpoints, and more. |
| **Security operations** | Backup/restore evidence, billing/spend alerts, registrar/DNS security, CAA and dangling-DNS checks, WAF/restricted admin access, canary detection, and independent security review evidence. |
| **Privacy & legal readiness** | Privacy/terms/refund/cookie disclosures, consent, data minimization, SDK review, dark-pattern checks, claims, accessibility, licensing, marketing opt-out, and deletion workflows. |
| **SEO & local discoverability** | Titles, descriptions, headings, canonicals, sitemap, robots, structured data, social previews, favicon, 404 pages, internal links, Search Console, local signals, image delivery, and legitimate backlink strategy. |
| **Trust & conversion** | Clear CTAs, short forms, pricing clarity, FAQs, service/product pages, real case studies, booking flows, confirmation states, response-time promises only when true, and visible contact details. |
| **Performance** | Image optimization, bundle size, loading states, API latency, layout stability, caching, database queries, pagination, and production-build performance. |
| **Responsive UX** | Mobile layouts, navigation, forms, tables, dialogs, touch targets, overflow, clickable contact details, and mobile optimization. |
| **Accessibility** | Keyboard navigation, focus states, contrast, semantic HTML, labels, alt text, motion, controls, and useful errors. |
| **Forms** | Client and server validation, invalid input, duplicate submissions, success/error messages, failures, mobile input, and spam/abuse cases. |
| **Trust & content integrity** | No fabricated testimonials, metrics, customer logos, certifications, capabilities, business details, pricing, reviews, or unsupported claims. |
| **Production cleanup** | Console errors, network failures, starter artifacts, placeholder text, unused navigation, debug mode, source maps, dependencies, configuration, and deployment readiness. |
| **Final verification** | A clear distinction between evidence-backed PASS/FAIL/UNKNOWN/N/A security results and broader production-readiness status. |

## 🔐 Evidence-Driven Security

Production Pup uses an evidence-driven **70-check security verification matrix**. The governing rule is simple: if you cannot point to the code, setting, configuration, test, or log that proves a guardrail exists, do not mark it PASS.

The security workflow also separates repository-checkable controls from operational/provider controls. Backups, restore tests, billing alerts, registrar/DNS security, WAF configuration, restricted admin access, canary detection, and independent penetration testing must be supported by external evidence rather than guessed from source code.

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
Privacy + legal pass
    ↓
SEO + accessibility pass
    ↓
Performance pass
    ↓
Trust + conversion pass
    ↓
Production pass
    ↓
Final visual + mobile audit
    ↓
Verify what is actually ready
```

A polished interface cannot compensate for broken authorization, leaked API keys, missing consent controls, fake claims, or broken user flows.

## ⚡ Slash Commands

Production Pup includes **user-invocable slash commands** for focused workflows. The commands use the main `SKILL.md` as their source of truth.

| Command | Purpose |
| --- | --- |
| `/production-pup` | Run the complete Production Pup audit. |
| `/fix` | Audit, implement relevant fixes, then verify them. |
| `/report` | Audit only and produce a structured readiness report. No project changes. |
| `/security` | Run the 70-check evidence-driven security workflow plus operational evidence checks. |
| `/seo` | Focus on SEO, metadata, crawling, structured data, social previews, local discoverability, and trust/conversion SEO. |
| `/performance` | Focus on frontend, API, database, caching, bundles, queries, and scalability. |
| `/design` | Focus on visual quality, design systems, UX correctness, motion, and anti-vibecoding patterns. |
| `/accessibility` | Focus on keyboard, semantic HTML, contrast, labels, motion, and accessible interaction. |
| `/polish` | Focus on website details, interaction correctness, micro-interactions, and mobile polish. |
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
/polish
```

Runs the focused website polish and interaction audit.

```text
/fix
```

Audits, fixes relevant issues, and verifies the changes.

```text
/report
```

Creates a report without modifying the project.

## 🛠️ How to Use

The main skill lives in `SKILL.md`. Focused slash-command workflows live directly under `.claude/commands/`. Detailed reference material lives under `references/`.

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
- improve trust and conversion flows
- review AI-agent permissions and production security

The preferred workflow is to invoke the relevant Production Pup command rather than manually pasting a long prompt.

## 🔍 The Production Standard

Production Pup does **not** say "production-ready" just because the page renders.

Before making that claim, the project should have:

- working core functionality
- protected secrets
- server-side authorization
- privileged-account protection where appropriate
- validated user input
- appropriate abuse and resource protection
- business logic enforced server-side
- safe concurrency and webhook processing where relevant
- controlled CI/CD credentials and dependencies
- secure AI inputs, outputs, tools, and agent permissions where AI exists
- privacy/legal controls appropriate to the product and jurisdiction
- intentional analytics and tracking
- useful SEO metadata on public pages
- accessible interactions
- responsive layouts without accidental overflow
- useful success and error feedback
- loading, empty, success, and error states
- optimized assets and reasonable performance
- real CTAs, contact details, booking/confirmation flows, and trust signals where applicable
- a clean production build
- no unexplained critical console or network errors
- no fake credibility or unsupported claims
- a coherent, product-specific visual system
- evidence for operational controls that cannot be verified from source code

If something cannot be verified, **say so instead of pretending it is done.**

## 🎨 Design Philosophy

Production Pup favors **intentional design over trend stacking**.

Gradients, glassmorphism, giant shadows, generic bento grids, decorative code windows, excessive animation, and other fashionable patterns are not automatically forbidden. They simply need a reason to exist.

> **Every major visual choice should earn its place.**

## 📋 Quick Pre-Launch Check

- [ ] Privacy Policy exists if required
- [ ] Terms/refund/cookie disclosures exist where applicable
- [ ] Consent flows match actual data collection
- [ ] No unnecessary personal data is collected
- [ ] Third-party SDKs are reviewed
- [ ] No frontend secrets
- [ ] HTTPS is configured
- [ ] Privileged accounts use MFA where supported
- [ ] Business logic and permissions are enforced server-side
- [ ] Webhooks are verified and safely deduplicated where used
- [ ] CI/CD credentials and actions are scoped
- [ ] AI data, output, tools, and agent permissions are controlled where used
- [ ] Page titles and descriptions are correct and unique
- [ ] Social preview is configured
- [ ] Favicon is present
- [ ] Sitemap and robots configuration are correct
- [ ] Images are optimized
- [ ] Performance has been checked
- [ ] Contrast has been checked
- [ ] Button states have readable text/icons
- [ ] Buttons and CTA groups do not overlap
- [ ] Mobile layout works without unintended horizontal overflow
- [ ] Mobile menu works
- [ ] Phone/email links are clickable where appropriate
- [ ] Logo/home navigation works where expected
- [ ] Tracking and cookie behavior is intentional
- [ ] Custom 404 exists
- [ ] Broken links and footer links are fixed
- [ ] Forms validate correctly
- [ ] Success and error messages are useful
- [ ] Placeholder text and unused navigation are removed
- [ ] Trust claims, reviews, case studies, pricing, and business details are real
- [ ] Booking flow and confirmation state work where applicable
- [ ] Keyboard navigation works
- [ ] Reduced-motion behavior is supported
- [ ] Production build has been tested
- [ ] Backups and restore tests are evidenced where relevant
- [ ] Provider/security controls are verified rather than assumed

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
│       ├── polish.md
│       └── launch.md
├── references/
│   ├── design-quality.md
│   ├── video-polish-checks.md
│   ├── privacy-legal-readiness.md
│   ├── trust-conversion-seo.md
│   └── security-operational-hardening.md
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
