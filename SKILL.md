---
name: production-pup
description: Turn vibecoded websites and web apps into production-ready products. Use before launching, shipping, reviewing, or polishing a website to audit security, privacy, SEO, accessibility, performance, responsive UX, copy, trust, technical cleanup, and launch readiness.
---

# Production Pup

Production Pup is a production-readiness quality gate for websites and web apps.

Do not stop at "it works." Inspect the product as a real user would. Apply only checks relevant to the project, verify what can be verified, identify what cannot be verified, and clearly report anything outstanding.

## When to Use

Use this skill when:

- launching or preparing to launch a website or web app
- reviewing a finished or nearly finished site
- polishing a vibecoded or AI-generated website
- fixing production-readiness issues
- preparing a landing page, SaaS product, dashboard, ecommerce site, portfolio, or web app for real users
- performing a final pre-launch audit

## 1. Understand the Product First

Before changing anything, determine:

- what the product actually does
- who uses it
- the primary user action or conversion goal
- required pages and routes
- data collected
- third-party services and integrations
- accounts, authentication, authorization, payments, or subscriptions
- applicable privacy and legal requirements
- intended brand and visual direction

Do not rewrite the existing stack without a concrete reason.

## 2. Anti-Vibe-Coding Design Audit

Treat these as anti-defaults, not absolute bans. Every major visual choice should have a reason.

Check for unnecessary use of:

1. harsh gradients
2. generic icon-library icons
3. pure white backgrounds everywhere
4. rainbow or arbitrary multi-color palettes
5. heavy drop shadows
6. generic three-feature-card layouts
7. emojis as UI icons
8. excessive glassmorphism or liquid glass
9. em dashes in normal product copy
10. overused AI-startup fonts such as Inter, Geist, or Space Grotesk by default
11. decorative colored side stripes
12. fake testimonials, customers, reviews, or social proof
13. generic bento grids
14. fake terminal/code windows used as decoration
15. formulaic "It's not X, it's Y" copy
16. checkmark bullets everywhere
17. three pricing tiers by default
18. sections that demonstrate nothing about the real product
19. excessively soft corner radii
20. purple + black as an automatic AI palette
21. missing skeleton/loading states for async experiences
22. decorative radial orbs
23. dot-grid backgrounds
24. sparkle icons used as generic AI decoration
25. animated arrows used only for flair
26. missing Terms of Service when required
27. missing Privacy Policy when required
28. hover animation on every interactive element
29. neon colors without a product reason
30. generic pastel palettes without a reason

Prefer a small, coherent design system over a collection of trendy effects.

## 3. Design System

Check consistency of typography, type scale, fonts, spacing, colors, surfaces, borders, radii, shadows, icons, buttons, forms, responsive breakpoints, and motion.

Avoid random radii, unrelated shadows, inconsistent buttons, arbitrary colors, multiple icon styles, and typography drift.

## 4. Security Audit

### Secrets

- Never expose private API keys in browser JavaScript.
- Keep secrets server-side.
- Verify environment variables are configured correctly.
- Ensure server-only variables are not exposed to clients.
- Search the repository and relevant Git history for keys, tokens, passwords, private keys, database URLs, connection strings, and credentials.
- If a real secret was committed, treat it as compromised and rotate/revoke it. Deleting the latest copy is not enough.

### Authentication and authorization

- Protect admin routes server-side.
- Enforce authentication on protected resources.
- Secure sessions, cookies, and tokens.
- Enforce object-level permissions so changing an ID cannot expose another user's data.
- Check for IDOR/BOLA-style access-control issues.

### Input and injection

- Validate important input server-side.
- Use schemas and allowlists where appropriate.
- Prevent XSS with safe output handling and sanitization when rich HTML is necessary.
- Use parameterized queries, prepared statements, or a safe ORM.
- Never concatenate untrusted input into SQL.
- Apply least-privilege database permissions.

### Abuse protection

Protect login, signup, password reset, public forms, expensive APIs, AI/model endpoints, email sending, and other abuse-prone endpoints with appropriate rate limits.

For metered services, set provider-side or application-level spending limits where possible. Do not expose unlimited expensive operations to unauthenticated users.

Use sensible spam protection such as rate limiting, honeypots, bot detection, or CAPTCHA/Turnstile-style systems when justified.

### File uploads

If uploads exist, validate size and type, do not trust client MIME types or filenames, store files safely, prevent inappropriate executable serving/execution, and consider malware scanning for higher-risk workflows.

### Browser and transport security

- Protect cookie-authenticated state-changing requests against CSRF.
- Avoid permissive `*` CORS for private/authenticated APIs.
- Use HTTPS in production.
- Check HTTP-to-HTTPS behavior and mixed content.
- Review CSP, HSTS, X-Content-Type-Options, Referrer-Policy, Permissions-Policy, and clickjacking protections as appropriate.
- Use `Secure`, `HttpOnly`, and appropriate `SameSite` cookie settings where applicable.
- Disable debug mode and prevent production exposure of stack traces, internal paths, secrets, debug endpoints, and development tooling.

## 5. Privacy, Cookies, and Tracking

- Provide an accurate Privacy Policy when required.
- Provide Terms of Service/Conditions when required.
- Document cookie/tracking practices when applicable.
- If consent is legally required, obtain it before relevant tracking starts and make choices understandable.
- Collect only data the product actually needs.
- Audit analytics, ads, pixels, session replay, cookies, SDKs, and third-party embeds.
- Review privacy, permissions, network requests, cookies, and performance impact of third-party embeds.

Never invent legal compliance or use fake legal text.

## 6. SEO and Discoverability

For public sites, audit:

- unique descriptive page titles
- useful page-specific meta descriptions
- one clear primary H1 per page where appropriate
- logical heading hierarchy
- clean, descriptive URL slugs
- intentional canonical URLs
- valid `sitemap.xml`
- correctly configured `robots.txt`
- accurate schema.org structured data where useful
- Open Graph/social preview metadata including `og:image`
- real favicon/app icons
- useful custom 404 page
- working internal links and routes
- appropriate `lang` attribute on the HTML element
- useful page source metadata and crawlable HTML
- `llms.txt` when useful for the site's AI-discovery strategy

Remember: `robots.txt` is not access control and must not be used to protect private data.

Do not fabricate structured data, reviews, ratings, customer counts, or other SEO-facing claims.

### Search-engine and crawler sanity checks

Watch for hidden launch problems such as:

- Vercel/preview URLs exposed as the canonical public URL
- framework starter URLs or branding left in metadata
- AI crawlers accidentally blocked when the project intentionally wants AI discovery
- all crawlers accidentally blocked
- multiple or conflicting H1 elements
- missing H1 entirely on pages that need one
- duplicate page titles
- missing descriptions
- missing canonical tags
- missing sitemap
- missing favicon
- missing `lang` attribution
- missing alt text

Do not automatically block AI crawlers. The correct policy depends on the site's goals, privacy requirements, licensing concerns, and content strategy.

## 7. Performance and Scalability Audit

Performance is not only about page load. Audit frontend rendering, assets, APIs, databases, caching, infrastructure, and scaling bottlenecks together.

### Frontend and asset performance

Check for:

- compressed and appropriately sized images
- modern image formats where useful
- lazy loading for below-the-fold or expensive media where appropriate
- minified JavaScript and CSS in production
- code splitting and sensible JavaScript chunks
- unnecessary dependencies and unused packages
- unnecessarily large JavaScript bundles
- unnecessary client-side work
- unnecessary React/component re-renders
- deferred loading of non-critical scripts
- excessive network requests
- layout shifts
- appropriate loading, empty, error, and success states

Do not remove loading states just to make a demo look smoother.

### API and application performance

- Cache API responses when data and freshness requirements make caching safe.
- Cache expensive computations and repeated database queries where appropriate.
- Compress API responses/payloads when supported and beneficial.
- Avoid sending fields or records the client does not need.
- Debounce high-frequency input handlers such as search, filtering, and autocomplete when appropriate.
- Paginate large lists instead of loading unbounded datasets.
- Lazy-load expensive features when not needed immediately.
- Defer non-critical scripts and work until after critical content is available.

Do not add caching blindly. Respect authentication, personalization, invalidation, freshness, and sensitive data requirements.

### Database performance

- Index columns used frequently for filtering, joins, sorting, and lookups when justified by query patterns.
- Inspect slow or expensive queries.
- Cache expensive queries when appropriate.
- Look for N+1 database queries, especially inside loops, nested resources, and list endpoints.
- Avoid fetching the same records repeatedly.
- Use pagination for large database-backed collections.
- Use database connection pooling for applications that make repeated database connections.
- Avoid over-indexing when write cost and storage overhead outweigh the benefit.

### Infrastructure and delivery

- Use a CDN for static assets and cacheable content when it materially improves latency or reduces origin load.
- Consider a load balancer when multiple application instances or traffic distribution are actually needed.
- Verify caching layers, CDN behavior, and cache invalidation.
- Check API and database latency under realistic production conditions.
- Test the production build rather than relying only on development-mode performance.

### Performance anti-patterns

Actively look for N+1 queries, unnecessary re-renders, unused dependencies, unbounded list fetching, uncompressed images or API payloads, blocking non-critical scripts, loading everything initially, repeated expensive queries without caching, missing indexes for proven bottlenecks, and excessive database connections instead of pooling.

Optimize actual bottlenecks rather than adding infrastructure because it is fashionable.

## 8. Mobile and Responsive UX

Test real small-screen layouts.

Check navigation, forms, buttons, text wrapping, images, cards, tables, modals, dialogs, horizontal overflow, touch targets, sticky/fixed elements, keyboard behavior, mobile inputs, mobile menus, and orientation changes where relevant.

A desktop-only site is not finished.

## 9. Accessibility

Check:

- keyboard navigation
- visible focus states
- sufficient color contrast
- semantic HTML
- accessible form labels
- meaningful button/link names
- correct link semantics
- useful alt text
- decorative images appropriately ignored by assistive technology
- reduced-motion support where relevant
- adequate touch targets
- readable text
- reasonable line length
- useful validation errors
- no reliance on color alone for state
- skip-to-content link where appropriate

Avoid vague controls such as "Click here" and unlabeled icon-only buttons.

## 10. Forms and Validation

Test important forms with empty submissions, invalid formats, excessively long input, unexpected characters, duplicate submissions, network failures, server errors, successful submissions, keyboard navigation, mobile input, and spam/abuse cases.

Also verify useful UX patterns where relevant:

- password visibility toggle
- clear inline errors
- success/confirmation states
- loading/disabled state during submission
- prevention of accidental double submission
- newsletter/contact confirmation
- copy-to-clipboard feedback

Client-side validation improves UX. Server-side validation is the security boundary. Use both.

## 11. Product Demonstration

If the site sells, explains, or promotes a real product, demonstrate the actual product.

Prefer real screenshots, realistic UI states, meaningful flows, interactive demos, and real before/after examples.

Do not substitute fake terminal windows, decorative dashboards, invented metrics, or fake testimonials for a real product demonstration.

## 12. Copywriting and Content Quality Audit

Treat copy as part of product quality. The site should be easy to understand quickly and should sound like a real product, not generated filler.

### Messaging

- Make the above-the-fold section communicate the product and value clearly.
- Use specific headlines instead of vague hype.
- Make the body copy support the headline rather than changing the promise.
- Put the benefit before the feature when explaining value.
- Write for scanning and impatient readers.
- Break up large blocks of text.
- Prefer one clear idea per section.
- Keep sections focused instead of mixing unrelated messages.
- Use roughly 1-3 important bullets per section when bullets genuinely help.
- Use punchy, precise copy rather than padded prose.
- Remove unnecessary information.
- Use generic openers sparingly and replace them with product-specific language.
- Speak to one clear buyer/user at a time instead of trying to address everyone.

### Calls to action

- CTAs should use a clear verb and communicate the expected outcome where useful.
- Handle important objections before the CTA when users need reassurance.
- Make the CTA understandable without requiring surrounding copy to decode it.
- Do not use vague CTAs when a specific action is possible.

### Avoid formulaic AI copy

Check for and rewrite:

- fabricated claims
- generic openers
- empty marketing adjectives
- aphorism-style formulas that sound manufactured
- repeated two-beat antithesis structures
- "It's not X, it's Y" constructions
- padded explanations that could be shorter
- unnecessary em dashes
- claims that have no evidence

The goal is not to ban a particular sentence structure. The goal is to make the writing sound specific, human, useful, and credible.

### Claims and credibility

Never invent customers, testimonials, reviews, ratings, user counts, revenue, case studies, logos, performance metrics, certifications, awards, integrations, business details, or product capabilities.

If a claim cannot be substantiated, remove it or rewrite it as an accurate non-quantified statement.

## 13. Content, Claims, and Trust

Use real business/contact information where required. Check licenses and rights for images, icons, fonts, videos, and other assets.

Never claim that a site is "100% secure," "fully compliant," "best in the world," or similar unless the claim is genuinely supportable and appropriately qualified.

## 14. Interaction and Polish

Verify useful production details where relevant:

- sticky header/navigation behaves correctly
- mobile menu opens, closes, and traps focus appropriately when needed
- dark-mode toggle actually persists and does not flash badly on load
- hover states exist where they improve desktop usability but are not required for touch devices
- focus states remain visible
- expandable FAQs work and are accessible
- back-to-top controls appear only when useful
- scroll progress indicators reflect actual page position
- cookie banner works and respects consent choices
- copy buttons provide success/error feedback
- newsletter signup provides a clear confirmation state
- destructive actions have appropriate confirmation/protection
- loading animations do not block usable content
- error and empty states tell the user what to do next

Do not add interactions just to make a page feel animated.

## 15. Technical Production Cleanup

Before shipping:

- run the production build
- fix meaningful browser console errors
- fix failed network requests
- remove starter/template branding
- remove placeholder copy
- remove development-only UI and tooling
- remove unnecessary dependencies
- review production source maps and debug artifacts
- verify environment-specific configuration
- verify error handling
- verify deployment configuration
- verify the production URL is used consistently in metadata and links
- check that preview/development URLs are not unintentionally exposed

## 16. Navigation and UX

Verify that:

- every important page is reachable
- navigation labels are clear
- active states make sense
- buttons actually perform their promised actions
- links do not lead to dead ends
- destructive actions are clear and appropriately protected
- success and error feedback is understandable
- users can recover from mistakes
- empty states explain what to do next
- internal links create sensible paths through the product

## 17. Final Pre-Launch Gate

Before declaring the project ready, verify as applicable:

- [ ] Core functionality works
- [ ] Authentication and permissions are correct
- [ ] Secrets are protected
- [ ] Inputs and APIs are protected
- [ ] Abuse/rate limits are considered
- [ ] HTTPS and browser security are configured
- [ ] Privacy/legal requirements are addressed
- [ ] SEO basics are complete
- [ ] Titles and meta descriptions are unique and useful
- [ ] H1/heading structure is sensible
- [ ] Canonical URLs exist where needed
- [ ] Sitemap and robots.txt are correct
- [ ] `lang` attribution exists
- [ ] Favicon and social metadata exist
- [ ] 404 and error states work
- [ ] Forms are validated
- [ ] Accessibility basics pass
- [ ] Mobile layouts and menus work
- [ ] Images/assets are optimized
- [ ] Loading/empty/error states exist
- [ ] API and database performance are reviewed
- [ ] Caching is used where appropriate
- [ ] Database indexes and query patterns are reviewed
- [ ] N+1 queries are checked
- [ ] Large lists are paginated
- [ ] CDN/load balancing are considered where appropriate
- [ ] Database connection pooling is configured where needed
- [ ] JavaScript/CSS are optimized for production
- [ ] Unused dependencies are removed
- [ ] Non-critical scripts are deferred where appropriate
- [ ] Above-the-fold messaging is clear
- [ ] Copy is scannable and specific
- [ ] CTAs are clear and outcome-oriented
- [ ] No formulaic/filler AI copy remains
- [ ] No fabricated claims or fake credibility remain
- [ ] Console/network errors are resolved
- [ ] Production build succeeds
- [ ] Real product content is present

## 18. How to Report the Audit

For each applicable area, classify the result as one of:

- **Implemented**: the requirement exists in the project.
- **Verified**: the requirement was tested or inspected successfully.
- **Provider handled**: responsibility belongs to the hosting/service provider and is not directly controllable in the codebase.
- **Not applicable**: the project genuinely does not need it.
- **Outstanding**: the requirement is missing, broken, or cannot yet be verified.

Do not claim something is secure, compliant, accessible, performant, or production-ready merely because the code looks correct. State what was actually checked and what remains uncertain.

## Core Rule

The goal is not to make every website look the same.

The goal is to make every shipped website feel **intentional, honest, usable, secure, accessible, technically clean, performant, scalable where needed, clear in its messaging, and ready for real users**.
