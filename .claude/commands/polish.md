# Production Pup: Polish

Run the focused website polish, interaction-correctness, micro-animation, content, and mobile audit.

Read `SKILL.md` first, then read:
- `references/video-polish-checks.md`
- `references/design-quality.md`
- `references/ui-vocabulary.md`
- `references/ai-content-authenticity.md`

Use these references as the source of truth for this workflow.

## Command

`/polish`

Use precise UI vocabulary when describing layout, components, interaction states, responsive behavior, and verification results.

## Website production checks

Check and, when requested, fix:

- horizontal scroll and mobile overflow
- broken links and footer links
- mobile menu
- favicon
- page titles and meta descriptions
- custom 404 page
- accurate copyright year where displayed
- compressed/optimized images
- broken buttons
- success and error messages
- placeholder text
- unused navigation
- clickable logo
- clickable phone numbers
- clickable email addresses
- overall mobile optimization

## UI correctness checks

Also inspect and, when requested, fix:

- button text/background contrast
- button icon/background contrast
- hover, focus, active, disabled, loading, success, and error states
- overlapping buttons and CTA groups
- hidden controls underneath visible controls
- pointer-event collisions
- flex/grid spacing and wrapping
- unsafe negative margins or absolute positioning
- responsive breakpoint collisions
- navigation and menu collisions
- modal/dropdown/tooltip stacking problems
- inconsistent iconography
- emoji used as UI icons
- Lucide/lucide-react used for new UI icons
- missing accessible names for icon-only controls
- inconsistent icon sizing and optical weight
- missing meaningful micro-interactions
- excessive/decorative animation
- reduced-motion support
- animation performance
- inconsistent timing/easing
- loading/success/error feedback
- overall interaction polish and perceived craftsmanship

## Content polish

Also inspect visible copy for generic AI-style filler, repetitive stock phrasing, unnecessary rhetorical questions, cliche framing, over-explaining obvious points, excessive emoji use, unsupported claims, and lack of project-specific substance.

Treat these as review signals, not proof of AI authorship. Do not add fake typos, awkward grammar, fake personal experience, fabricated examples, or invented claims to make copy appear human.

## Animation guidance

For React projects, prefer Motion when appropriate, using the current `motion` package and `motion/react` imports. Use it for purposeful hover, tap, focus, in-view, layout, enter/exit, and gesture interactions. Use CSS transitions when a simple effect is clearer and lighter. Do not stack animation libraries without a concrete reason.

Do not add animation merely to make the site look busy. Motion should communicate state, hierarchy, continuity, or feedback.

## Icon guidance

Do not use emoji characters as UI icons.

Do not introduce Lucide/lucide-react for new UI icons. Prefer one deliberate icon family such as Phosphor, Radix Icons, Heroicons, Tabler, or a project-specific/custom SVG system. Keep icon weight and sizing consistent.

## Verification

After fixes:

1. Test important controls at desktop and narrow mobile widths.
2. Hover and focus button groups.
3. Tab through interactive elements.
4. Verify separate clickable hit areas.
5. Test menus, overlays, dialogs, and dropdowns.
6. Check for horizontal overflow and breakpoint collisions.
7. Test reduced-motion behavior.
8. Check the browser console.
9. Re-run the relevant build/tests.
10. Compare important copy against the actual product and evidence.

Never solve a structural overlap bug by adding arbitrary z-index values unless the stacking context is actually intentional.

Arguments: $ARGUMENTS
