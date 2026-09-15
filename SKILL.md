---
name: production-pup
description: Turn vibecoded websites and web apps into production-ready products. Use before launching, shipping, reviewing, or polishing a website to audit security, privacy, SEO, accessibility, performance, responsive UX, trust, technical cleanup, and launch readiness.
---

# Production Pup

Production Pup is a production-readiness quality gate for websites and web apps.

Do not stop at "it works." Before declaring a project ready, inspect the product as a real user would and audit the areas that apply. Do not blindly satisfy every checklist item. Verify what can be verified, identify what cannot be verified, and clearly report anything still outstanding.

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
- the intended brand and visual direction

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
8. excessive glassmorphism or "liquid glass"
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

Check consistency of:

- typography and type scale
- font choices
- spacing
- colors
- backgrounds and surfaces
- borders
- radius scale
- shadows
- icon style
- button hierarchy
- form controls
- responsive breakpoints
- motion behavior

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

If uploads exist:

- validate size and type
- do not trust client MIME types
- do not trust filenames
- store files safely
- prevent inappropriate executable serving/execution
- consider malware scanning for higher-risk workflows

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
- Review the privacy, permissions, network requests, cookies, and performance impact of third-party embeds.

Never invent legal compliance or use fake legal text.

## 6. SEO and Discoverability

For public sites, audit:

- unique descriptive page titles
- useful page-specific meta descriptions
- logical heading hierarchy
- intentional canonical URLs
- valid `sitemap.xml`
- correctly configured `robots.txt`
- accurate schema.org structured data where useful
- Open Graph/social preview metadata
- real favicon/app icons
- useful custom 404 page
- working internal links and routes

Remember: `robots.txt` is not access control and must not be used to protect private data.

Do not fabricate structured data, reviews, ratings, customer counts, or other SEO-facing claims.

## 7. Performance and Scalability Audit

Performance is not only about making a page load faster. Audit frontend rendering, assets, APIs, databases, caching, infrastructure, and scaling bottlenecks together.

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
- expensive components rendering when they do not need to
- unnecessary React/component re-renders
- deferred loading of non-critical scripts
- excessive network requests
- layout shifts
- appropriate loading, empty, error, and success states

Do not remove loading states just to make a demo look smoother.

### API and application performance

- Cache API responses when the data and freshness requirements make caching safe.
- Cache expensive computations and repeated database queries where appropriate.
- Compress API responses/payloads when supported and beneficial.
- Avoid sending fields or records the client does not need.
- Debounce high-frequency input handlers such as search, filtering, and autocomplete when appropriate.
- Paginate large lists instead of loading unbounded datasets into the browser.
- Lazy-load expensive features when they are not needed immediately.
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
- Avoid over-indexing tables when the write cost and storage overhead outweigh the benefit.

### Infrastructure and delivery

- Use a CDN for static assets and other cacheable content when it materially improves latency or reduces origin load.
- Consider a load balancer when the application needs multiple application instances or traffic distribution. Do not add one to a small single-instance app without a scaling requirement.
- Verify caching layers, CDN behavior, and cache invalidation.
- Check API and database latency under realistic production conditions.
- Test the production build rather than relying only on development-mode performance.

### Performance anti-patterns

Actively look for:

- N+1 database queries
- unnecessary re-renders
- unused dependencies
- unbounded list fetching
- uncompressed images or API payloads
- blocking non-critical scripts
- loading everything on the initial page
- expensive queries executed repeatedly without caching
- missing database indexes for proven query bottlenecks
- opening excessive database connections instead of pooling

Do not optimize based on fashion. Identify the actual bottleneck, then apply the simplest fix that improves it.

## 8. Mobile and Responsive UX

Test real small-screen layouts.

Check navigation, forms, buttons, text wrapping, images, cards, tables, modals, dialogs, horizontal overflow, touch targets, sticky/fixed elements, keyboard behavior, and mobile inputs.

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

Avoid vague controls such as "Click here" and unlabeled icon-only buttons.

## 10. Forms and Validation

Test important forms with:

- empty submissions
- invalid formats
- excessively long input
- unexpected characters
- duplicate submissions
- network failures
- server errors
- successful submissions
- keyboard navigation
- mobile input
- spam and abuse cases

Client-side validation improves UX. Server-side validation is the security boundary. Use both.

## 11. Product Demonstration

If the site sells, explains, or promotes a real product, demonstrate the actual product.

Prefer real screenshots, realistic UI states, meaningful flows, interactive demos, and real before/after examples.

Do not substitute fake terminal windows, decorative dashboards, invented metrics, or fake testimonials for a real product demonstration.

## 12. Content, Claims, and Trust

Never manufacture credibility.

Do not invent:

- customers
- testimonials
- reviews
- ratings
- user counts
- revenue
- case studies
- company logos
- performance metrics
- certifications
- awards
- integrations
- business details
- product capabilities

Remove unsupported claims such as "10x faster", "100% secure", "best in the world", or invented usage numbers unless they can be substantiated.

Use real business/contact details where required. Check licenses and rights for images, icons, fonts, videos, and other assets.

## 13. Technical Production Cleanup

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

## 14. Navigation and UX

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

## 15. Final Pre-Launch Gate

Before declaring the project ready, verify as applicable:

- [ ] Core functionality works
- [ ] Authentication and permissions are correct
- [ ] Secrets are protected
- [ ] Inputs and APIs are protected
- [ ] Abuse/rate limits are considered
- [ ] HTTPS and browser security are configured
- [ ] Privacy/legal requirements are addressed
- [ ] SEO basics are complete
- [ ] Favicon and social metadata exist
- [ ] 404 and error states work
- [ ] Forms are validated
- [ ] Accessibility basics pass
- [ ] Mobile layouts work
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
- [ ] Console/network errors are resolved
- [ ] No fake credibility or unsupported claims remain
- [ ] Production build succeeds
- [ ] Real product content is present

## 16. How to Report the Audit

For each applicable area, classify the result as one of:

- **Implemented**: the requirement exists in the project.
- **Verified**: the requirement was tested or inspected successfully.
- **Provider handled**: responsibility belongs to the hosting/service provider and is not directly controllable in the codebase.
- **Not applicable**: the project genuinely does not need it.
- **Outstanding**: the requirement is missing, broken, or cannot yet be verified.

Do not claim something is secure, compliant, accessible, or production-ready merely because the code looks correct. State what was actually checked and what remains uncertain.

## Core Rule

The goal is not to make every website look the same.

The goal is to make every shipped website feel **intentional, honest, usable, secure, accessible, technically clean, performant, scalable where needed, and ready for real users**.
