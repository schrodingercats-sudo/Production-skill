# Production Pup: Video-Derived Website Polish Checks

These checks were extracted from the supplied video titled “20 things to tell Claude to fix on your vibecoded website”. They complement the main Production Pup skill and should be applied when relevant.

## 20 Checks

1. **No unintended horizontal scroll**
   - Check desktop and mobile for accidental horizontal overflow.
   - Fix elements wider than the viewport, overflow caused by media, tables, navigation, or fixed-width components.

2. **Find broken links**
   - Test internal navigation and important external links.
   - Remove or repair dead destinations and incorrect paths.

3. **Add a mobile menu**
   - If desktop navigation does not fit on small screens, provide a usable mobile navigation pattern.
   - Ensure it opens, closes, and remains keyboard accessible.

4. **Add a favicon**
   - Provide an intentional favicon/app icon and verify it loads in production.

5. **Fix page titles**
   - Use accurate, page-specific titles instead of generic or duplicated titles.

6. **Add meta description**
   - Add useful page-specific descriptions for public pages where appropriate.

7. **Fix footer links**
   - Verify footer links point to real, intended destinations.
   - Remove placeholder or dead footer navigation.

8. **Custom 404 page**
   - Provide a useful branded 404/error page with a recovery path.

9. **Copyright year**
   - Check that a displayed copyright year is accurate and maintained rather than becoming stale.
   - Do not add a copyright notice when the project has no reason to display one.

10. **Compress images**
    - Optimize oversized images and use appropriate dimensions/formats without destroying required quality.

11. **Fix broken buttons**
    - Every important button must perform the action its label promises.
    - Check disabled, loading, success, and failure behavior where relevant.

12. **Success messages**
    - Important successful actions should communicate completion clearly.

13. **Error messages**
    - Failed actions should provide useful, understandable feedback and a next step where possible.

14. **Remove placeholder text**
    - Remove lorem ipsum, “coming soon” filler, template copy, fake labels, and other unfinished content before launch.

15. **Remove unused navigation**
    - Remove navigation items that do not lead anywhere or do not serve a real user need.

16. **Fix mobile overflow**
    - Explicitly test narrow viewport behavior, including text, images, tables, dialogs, navigation, and fixed-position elements.

17. **Clickable logo**
    - When the logo functions as site identity/navigation, make it a meaningful link to the appropriate home/root destination.

18. **Clickable phone number**
    - Where a real phone number is presented for contact, use an appropriate `tel:` link so supported devices can initiate a call.

19. **Clickable email**
    - Where a real email address is presented for contact, use an appropriate `mailto:` link when that matches the intended UX.

20. **Mobile optimize**
    - Treat mobile as a first-class production target: responsive layout, readable text, usable controls, correct spacing, touch targets, menus, media, forms, and no accidental overflow.

## Conditional product-completeness sweep

The videos also suggest features that are easy to overlook. These are **conditional checks**, not a mandate to add every feature to every website. Add them only when they solve a real user need or are part of the product's intended behavior.

- **Dark-mode toggle:** if offered, persist the choice, maintain contrast in both themes, and avoid a disruptive initialization flash.
- **Site search:** where users need to find substantial content or records, verify results, empty/loading/error states, and safe query handling.
- **Primary CTA and top-of-page clarity:** make the main action and product value clear without stacking competing CTAs.
- **Announcement/banner:** if present, ensure it can be dismissed when appropriate and does not cover navigation/content on mobile.
- **Skip-to-content:** provide a visible-on-focus skip link for keyboard users on sites with repeated navigation.
- **Print stylesheet:** for pages users may print/save, avoid clipping, wasteful dark backgrounds, and controls that obscure content.
- **Visibility toggles:** password reveal or show/hide controls must expose state accessibly and preserve input/state.
- **Expandable sections:** accordions/disclosures must communicate expanded state, work with keyboards, and not hide critical information unexpectedly.
- **Form completion:** verify pending/loading, validation failure, server failure, success, duplicate submission, and recovery after errors.
- **Copy/export actions:** show success/failure feedback and ensure the output is the intended data.
- **Confirmation dialogs:** use for destructive or hard-to-reverse actions; avoid unnecessary confirmation for routine reversible actions.
- **Floating contact/help controls:** ensure they do not cover primary controls or keyboard focus and work on mobile.
- **Tracking and consent:** analytics/marketing scripts must respect the site's consent and privacy requirements.
- **Scroll progress/back-to-top:** use only when useful for long pages; keep the indicator accurate and motion accessible.
- **Sticky navigation:** verify it does not cover anchor targets, focused controls, dialogs, or content on small screens.
- Do not add search, contact widgets, print controls, banners, or other features solely to satisfy a checklist. Mark them not applicable when they do not serve the product.

## Evidence and Fix Rules

- Do not mark a check PASS merely because the UI looks correct.
- For links, buttons, menus, forms, and error/success states, test the actual interaction where possible.
- Treat the red-X items shown in the source video as explicit anti-patterns: unintended horizontal scroll, placeholder text, and unused navigation should be removed rather than accepted as harmless.
- These are additions to Production Pup, not replacements for the security, accessibility, SEO, performance, or launch gates.
