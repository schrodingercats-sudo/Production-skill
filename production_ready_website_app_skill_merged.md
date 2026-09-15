# Production-Ready Website & App Launch Skill

## Purpose

When building, reviewing, fixing, or launching a website or web app, do
not stop at "it works."

The finished product should be: - functional - intentional in design -
secure - accessible - legally/privacy aware - SEO-ready - performant -
mobile-friendly - technically clean - honest about its capabilities -
ready for real users

Use this skill as a **pre-launch gate**, not as a list to blindly
satisfy. Apply only checks relevant to the project, verify them where
possible, and clearly flag anything that cannot be verified.

------------------------------------------------------------------------

# 1. Product Understanding Comes First

Before changing the project, identify:

-   What the product actually does
-   Who uses it
-   The main user action or conversion goal
-   What pages/routes are required
-   What data is collected
-   What third-party services are used
-   What payments, subscriptions, or accounts exist
-   What authentication/authorization is required
-   What legal/privacy requirements apply
-   What integrations are required
-   What brand and visual direction fits the product

Do not choose a visual style or technical architecture before
understanding the product.

Do not rewrite the existing stack without a concrete reason.

------------------------------------------------------------------------

# 2. Anti-Vibe-Coding Design Rules

Avoid using fashionable patterns as automatic defaults.

Do not blindly reach for:

1.  Harsh or unnecessary gradients
2.  Generic icon-library icons when a better visual treatment exists
3.  Pure white backgrounds everywhere
4.  Rainbow or multi-color palettes without a reason
5.  Heavy drop shadows
6.  Generic three-feature-card layouts
7.  Emojis as substitute UI icons
8.  Excessive glassmorphism / "liquid glass"
9.  Em dashes in normal product copy
10. Overused AI-startup fonts such as Inter, Geist, or Space Grotesk by
    default
11. Decorative colored side stripes without structural purpose
12. Fake testimonials, fake customers, fake reviews, or invented social
    proof
13. Generic bento grids used only because they are trendy
14. Fake terminal/code windows used as decoration
15. Formulaic copy such as "It's not X, it's Y"
16. Checkmark bullets everywhere
17. Three pricing tiers by default
18. Sections that demonstrate nothing about the real product
19. Excessively soft/rounded corner radii
20. Purple + black as an automatic AI palette
21. Removing skeleton/loading states from async experiences
22. Decorative radial orbs without purpose
23. Dot-grid backgrounds as generic decoration
24. Sparkle icons as generic "AI magic"
25. Animated arrows used only for flair
26. Missing Terms of Service when the product requires them
27. Missing Privacy Policy when personal data is collected or otherwise
    required
28. Hover animations on every interactive element
29. Neon colors without a product/brand reason
30. Generic pastel palettes without a reason

### Important nuance

These are **anti-default rules**, not absolute bans.

A gradient, icon library, rounded card, animation, glass effect, or
specific font can be correct when it serves the product.

The actual rule is:

> Every major visual choice should have a reason.

Prefer a small, coherent visual system over a pile of trendy effects.

------------------------------------------------------------------------

# 3. Design System

Create a deliberate design system.

Define:

-   Typography and type scale
-   Font choices
-   Spacing scale
-   Color palette
-   Background/surface treatment
-   Border treatment
-   Radius scale
-   Shadows
-   Icon style
-   Button hierarchy
-   Form controls
-   Responsive breakpoints
-   Motion behavior

Avoid design-system drift.

Do not mix: - random corner radii - unrelated shadows - inconsistent
button shapes - multiple icon styles - arbitrary colors - unrelated
typography systems

Consistency beats decoration.

------------------------------------------------------------------------

# 4. Security Audit

Before launch, audit every applicable security area.

## Secrets and credentials

### 4.1 Hide API keys

Never expose private API keys in browser JavaScript.

Keep secrets server-side.

Only use public/publishable keys client-side when the provider
explicitly supports them.

### 4.2 Check environment variables

Verify: - required secrets are loaded from environment/configuration -
credentials are not hard-coded - server-only environment variables are
not exposed to the client - production configuration is different from
development where necessary

### 4.3 Check repository history

Search the repository and relevant Git history for: - API keys -
tokens - passwords - private keys - database URLs - connection strings -
service credentials

If a real secret was committed, assume it is compromised. Rotate/revoke
it. Simply deleting it from the latest commit is not enough.

------------------------------------------------------------------------

## Authentication and authorization

### 4.4 Protect admin routes

Admin access must be enforced server-side.

Hiding an admin link in the UI is not security.

### 4.5 Protect authenticated resources

Enforce authentication on protected resources.

Handle sessions, cookies, and tokens securely.

### 4.6 Enforce object-level permissions

Prevent users from changing an ID and accessing or modifying another
user's data.

Check for IDOR/BOLA-style vulnerabilities.

------------------------------------------------------------------------

## Input and injection protection

### 4.7 Validate user input

Validate important inputs server-side.

Use schemas/allowlists where appropriate.

Never trust client-side validation alone.

### 4.8 Prevent XSS

-   Escape output by default
-   Avoid unsafe HTML injection
-   Sanitize user-provided HTML if rich text is necessary
-   Review dangerous DOM APIs and templating escape hatches

### 4.9 Prevent SQL injection

Use: - parameterized queries - prepared statements - or a safe ORM

Never concatenate untrusted input into SQL.

### 4.10 Check database permissions

Ensure users can only read/write records they are authorized to access.

Use least-privilege database credentials.

------------------------------------------------------------------------

## Abuse protection

### 4.11 Rate limiting

Protect abuse-prone endpoints such as: - login - password reset -
signup - contact forms - expensive API endpoints - AI/model endpoints -
email sending - public submission endpoints

Use sensible per-user/IP/device limits where appropriate.

### 4.12 Spending and cost limits

For metered services, set provider-side or application-level limits
where possible.

This is especially important for: - AI/model APIs - email - storage -
paid APIs - image/video processing

Do not expose an unlimited expensive operation to unauthenticated users.

### 4.13 Spam protection

Protect public forms and submissions against spam.

Use appropriate measures such as: - rate limits - bot detection -
honeypots - CAPTCHA/Turnstile-style systems where justified -
server-side validation

Do not make every form miserable to use just to stop a few bots.

------------------------------------------------------------------------

## File handling

### 4.14 Secure uploads

If the product accepts files:

-   validate file size
-   validate file type
-   do not trust client MIME types
-   do not trust filenames
-   store uploads safely
-   prevent executable files from being served/executed where
    inappropriate
-   consider malware scanning for higher-risk workflows

------------------------------------------------------------------------

## Browser and transport security

### 4.15 CSRF protection

Protect cookie-authenticated state-changing requests against CSRF.

Use framework-native protection where available.

### 4.16 CORS

Do not use permissive `*` CORS for authenticated/private APIs unless
there is a deliberate reason.

Allow only required origins, methods, and headers.

### 4.17 HTTPS

Production traffic should use HTTPS.

Check: - HTTP → HTTPS redirects where appropriate - no mixed content -
secure API endpoints - secure third-party integrations

### 4.18 Security headers

Review appropriate headers, including:

-   Content-Security-Policy
-   Strict-Transport-Security
-   X-Content-Type-Options
-   Referrer-Policy
-   Permissions-Policy
-   frame-ancestors / clickjacking protections

### 4.19 Secure cookies

Where applicable:

-   `Secure`
-   `HttpOnly`
-   appropriate `SameSite`
-   narrow cookie scope

### 4.20 Disable debug mode

Production must not expose: - stack traces - internal paths - secrets -
verbose errors - debug endpoints - development tooling

------------------------------------------------------------------------

# 5. Privacy, Cookies, Tracking, and Data Collection

Do not treat privacy as a decorative footer link.

## 5.1 Privacy Policy

If personal data is collected or the product requires one, provide a
real Privacy Policy page.

It should accurately describe actual data practices.

Do not use fake legal text or claim compliance that has not been
established.

## 5.2 Terms & Conditions

If the product/business requires terms, provide a Terms & Conditions /
Terms of Service page.

## 5.3 Cookie policy

If cookies/tracking are used or a cookie policy is required, provide
appropriate information.

## 5.4 Cookie consent

If consent is legally required for particular cookies/tracking:

-   ask for consent before the relevant tracking starts
-   make the choice understandable
-   do not disguise consent
-   do not use preselected consent where inappropriate
-   provide a way to manage/revisit choices where required

## 5.5 Minimize data collection

Only collect data that the product actually needs.

Do not collect "just in case" data.

## 5.6 Tracking audit

Check: - analytics scripts - advertising trackers - pixels - session
replay - third-party embeds - cookies - SDKs

Know what each one sends and why it exists.

## 5.7 Third-party embeds

Audit every third-party embed.

Examples: - maps - videos - forms - social widgets - analytics - payment
widgets - chat widgets

Check: - privacy implications - permissions - network requests - cookie
behavior - performance - whether the embed is actually needed

------------------------------------------------------------------------

# 6. SEO and Discoverability

For public websites, perform an SEO audit.

## 6.1 Page titles

Every important page should have a unique, descriptive title.

Avoid: - "Home" - "Website" - framework defaults - duplicated titles

## 6.2 Meta descriptions

Add useful, page-specific descriptions where appropriate.

Do not keyword-stuff.

## 6.3 Headings

Use meaningful headings with logical hierarchy.

Do not skip heading levels just for visual sizing.

## 6.4 Canonical URLs

Set canonical URLs intentionally where duplicate/variant URLs could
exist.

## 6.5 Sitemap

Provide `sitemap.xml` for appropriate public sites.

Ensure it contains real, indexable URLs.

## 6.6 Robots

Configure `robots.txt` appropriately.

Do not accidentally block the entire production site.

Do not expose private routes simply because robots.txt hides them.
Robots.txt is not an access-control system.

## 6.7 Structured data

Use schema.org structured data when it genuinely describes the page.

Possible types include: - Organization - Product - Article -
BreadcrumbList - LocalBusiness - FAQ where appropriate

Never fabricate structured data.

## 6.8 Social preview

Provide appropriate Open Graph/social metadata.

Use a real social preview image for important pages.

Check that: - title is correct - description is correct - image is
valid - URL is correct

## 6.9 Favicon

Add a real favicon/app icon.

Do not leave framework starter icons in production.

## 6.10 404 page

Create a useful custom 404 page.

It should help the user recover rather than simply display an error.

## 6.11 Broken links

Test internal links.

Fix: - dead routes - incorrect anchors - stale URLs - navigation links
that lead nowhere

------------------------------------------------------------------------

# 7. Performance

Performance is part of product quality.

## 7.1 Compress images

Optimize images appropriately.

Use modern formats when beneficial.

Do not ship enormous images when a smaller asset will look identical.

## 7.2 Check page-load speed

Test realistic production builds.

Look at: - initial load - largest content - JavaScript execution - image
loading - API latency - layout shifts

## 7.3 Bundle hygiene

-   Avoid unnecessarily huge JavaScript bundles
-   Lazy-load expensive features where appropriate
-   Split code when useful
-   Remove unused dependencies
-   Avoid shipping large libraries for tiny features when native APIs
    are sufficient

## 7.4 Loading states

Async content should have appropriate: - loading states - skeletons
where useful - empty states - error states - success states

Do not remove loading states simply because they make a demo look less
polished.

------------------------------------------------------------------------

# 8. Mobile and Responsive Design

Test the actual product on small screens.

Check:

-   navigation
-   forms
-   buttons
-   text wrapping
-   images
-   cards
-   tables
-   modals
-   dialogs
-   horizontal overflow
-   touch targets
-   fixed/sticky elements
-   keyboard behavior

A site that only looks good on desktop is not finished.

------------------------------------------------------------------------

# 9. Accessibility

A polished product must also be usable.

Check:

-   keyboard navigation
-   visible focus states
-   color contrast
-   semantic HTML
-   accessible form labels
-   meaningful button labels
-   correct link semantics
-   alt text
-   reduced-motion support where relevant
-   touch target size
-   readable text size
-   reasonable line length
-   useful validation errors

## 9.1 Contrast

Check text and interactive elements for sufficient contrast.

Do not choose colors only because they look good in a design mockup.

## 9.2 Images

Meaningful images need useful alt text.

Decorative images should have an appropriate empty/ignored alternative
so screen readers do not announce irrelevant decoration.

## 9.3 Forms

Forms should be: - keyboard friendly - clearly labeled - logically
ordered - easy to understand - properly validated - usable without hover

Error messages should explain what went wrong and how to fix it.

## 9.4 Buttons and controls

Use clear labels.

Avoid vague controls such as: - "Click here" - unlabeled icon-only
buttons - ambiguous symbols

Do not rely on color alone to communicate state.

------------------------------------------------------------------------

# 10. Forms and Validation

Every important form should be tested as a real user would use it.

Test:

-   empty submissions
-   invalid formats
-   excessively long values
-   unexpected characters
-   duplicate submissions
-   network failure
-   server errors
-   successful submission
-   keyboard navigation
-   mobile input
-   spam/abuse cases

Client-side validation improves UX.

Server-side validation provides the security boundary.

You need both.

------------------------------------------------------------------------

# 11. Product Demonstration

If the website sells, explains, or promotes a real product, show the
product actually doing something.

Prefer:

-   real screenshots
-   real UI states
-   realistic flows
-   real before/after examples
-   interactive demos
-   meaningful sample data

Do not replace a product demonstration with:

-   fake terminal windows
-   random dashboard cards
-   decorative code
-   invented metrics
-   fake testimonials

------------------------------------------------------------------------

# 12. Content, Claims, and Trust

This is a hard rule:

**Never manufacture credibility.**

Do not invent:

-   customer names
-   testimonials
-   reviews
-   ratings
-   user counts
-   revenue
-   case studies
-   company logos
-   performance metrics
-   certifications
-   awards
-   integrations
-   business details
-   product capabilities

## 12.1 Remove fake reviews

If reviews are not real, remove them.

If real reviews exist, represent them accurately.

## 12.2 Remove unsupported claims

Remove or rewrite claims that cannot be supported.

Examples: - "10x faster" - "used by 50,000 companies" - "bank-grade
security" - "100% secure" - "best in the world"

Do not make claims simply because they sound convincing.

## 12.3 Real business details

Where a business website needs contact/business information, use real
information.

Do not fabricate: - addresses - phone numbers - company registration
details - staff - locations - partnerships

## 12.4 Copyright and asset rights

Check images, icons, fonts, videos, and other assets.

Do not use copyrighted assets without appropriate rights/license.

Do not assume that an image being available online means it is free to
use.

------------------------------------------------------------------------

# 13. Technical Production Cleanup

Before shipping:

-   Build the production version
-   Fix meaningful browser console errors
-   Fix network failures
-   Remove starter/template branding
-   Remove placeholder text
-   Remove development-only dependencies where appropriate
-   Remove unnecessary source maps when they expose information you do
    not intend to publish
-   Verify environment-specific configuration
-   Verify API endpoints
-   Verify database connections
-   Verify authentication/session configuration
-   Verify third-party integrations
-   Verify storage configuration
-   Verify error handling

### Console cleanliness

Investigate:

-   failed network requests
-   hydration errors
-   missing keys
-   accessibility warnings
-   deprecated APIs
-   CORS errors
-   unhandled promise rejections
-   runtime exceptions

Do not suppress errors simply to make the console look clean.

------------------------------------------------------------------------

# 14. Navigation and User Experience

Check the complete user journey.

A user should be able to:

-   understand what the product does
-   find the main action
-   navigate between important pages
-   recover from mistakes
-   understand errors
-   return from dead ends
-   find support/contact information where appropriate
-   use the site without depending on hover

Important information should not be hidden behind clever interactions.

Animation should communicate: - state - hierarchy - continuity -
feedback

Do not animate everything because the page feels empty.

------------------------------------------------------------------------

# 15. Pre-Launch 20-Point Quick Audit

Before launching, run this condensed checklist:

1.  Privacy Policy exists if required
2.  Terms & Conditions exists if required
3.  Secrets are not exposed in the frontend
4.  HTTPS is enabled
5.  Important pages have correct titles/descriptions
6.  Social preview image exists
7.  Favicon exists
8.  Sitemap and robots configuration are correct
9.  Images are compressed
10. Page-load speed has been checked
11. Color contrast has been checked
12. Site is mobile friendly
13. Cookie consent/tracking behavior is correct
14. Custom 404 page exists
15. Broken links are fixed
16. Forms have validation
17. Spam protection exists where needed
18. Analytics/tracking is intentional and consent-aware where required
19. Accessibility and keyboard navigation have been checked
20. Real claims, business details, and assets are used

This is a quick audit, not a replacement for the detailed checks above.

------------------------------------------------------------------------

# 16. Pre-Ship Procedure

When asked to build, finish, review, or launch a website, follow this
order.

## Step 1: Understand

Identify: - product - users - goals - routes - data - integrations -
legal/privacy requirements - brand direction

## Step 2: Inspect

Check: - framework - routing - dependencies - environment variables -
API routes - authentication - database - deployment - existing design
system

Do not rewrite blindly.

## Step 3: Build the foundation

Implement: - routing - real data flow - authentication/authorization -
forms - validation - loading states - error handling - responsive
behavior

## Step 4: Apply intentional design

Use a product-specific visual language.

Avoid generic AI-generated design defaults.

## Step 5: Security pass

Run the security audit.

Never expose secrets.

Never rely on client-side authorization.

Never trust client input.

## Step 6: Privacy pass

Review: - personal data - cookies - analytics - tracking - third-party
embeds - consent - privacy/legal pages

## Step 7: SEO/accessibility pass

Review: - titles - descriptions - headings - canonical URLs - structured
data - sitemap - robots - favicon - social metadata - alt text -
contrast - keyboard navigation - focus states - form labels

## Step 8: Performance pass

Check: - image sizes - page load - bundle size - API latency - loading
states - layout stability

## Step 9: Production pass

Test: - production build - console - network requests - environment
configuration - debug mode - starter artifacts - broken links - 404
behavior - mobile layout

## Step 10: Trust pass

Remove: - fake reviews - fake metrics - fake customer logos -
unsupported claims - fake business details - unlicensed assets

## Step 11: Final visual audit

Look at the complete site as a real user.

Ask:

-   Does this look like a real product rather than an AI-generated
    template?
-   Is the hierarchy obvious?
-   Is every decorative element earning its place?
-   Are the claims real?
-   Are animations useful?
-   Does the visual system feel consistent?
-   Does it work on mobile?
-   Does it remain good without unnecessary gradients, glow, glass, or
    animation?

------------------------------------------------------------------------

# 17. Verification Standard

Do not claim something is "secure," "accessible," "SEO optimized," or
"production-ready" merely because code for it exists.

For every applicable requirement:

-   **Implemented**: it is actually implemented
-   **Verified**: it was tested/confirmed
-   **Provider/framework handled**: a trusted dependency clearly handles
    it
-   **Not applicable**: explain why
-   **Outstanding**: it still needs work

If you cannot verify something, say so.

**Accuracy beats confidence. Verification beats assumption. Intentional
design beats trend stacking.**
