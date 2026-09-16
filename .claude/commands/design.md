# Production Pup: Design

Run the design, anti-vibecoding, UI-correctness, and interaction-focused Production Pup audit.

Read `SKILL.md` first and use its Anti-Vibe-Coding Design Audit and Design System sections as the source of truth. Then read `references/design-quality.md` for the detailed button, layout, icon, and micro-interaction checks.

## Command

`/design`

Audit and, when requested, fix:

- visual hierarchy
- typography and type scale
- spacing and layout consistency
- color system and contrast
- backgrounds and surfaces
- borders, radii, and shadows
- icon consistency and icon-library choices
- button and form hierarchy
- button text/background contrast
- button hover/focus/active/disabled states
- overlapping buttons and CTA groups
- pointer-event collisions and hidden controls
- flex/grid wrapping and responsive breakpoint collisions
- navigation, dropdown, modal, tooltip, and overlay stacking
- responsive breakpoints
- meaningful motion and reduced-motion behavior
- micro-interactions that communicate state
- animation performance and restraint
- generic AI/vibecoded visual patterns
- harsh gradients, excessive glassmorphism, decorative orbs and dot grids
- generic bento grids and three-card layouts
- fake terminal windows
- emoji UI icons
- Lucide/lucide-react used for new UI icons
- excessive sparkle/arrow decoration
- fake testimonials and metrics
- generic AI copy
- unexplained visual trends

### Interaction quality rule

A design is not considered polished if controls collide, overlap, become unreadable on hover, or share the same clickable area. Verify actual interaction states and hit targets, not only the static screenshot.

### Animation rule

For React projects, prefer Motion when appropriate for purposeful micro-interactions such as hover, tap, focus, in-view, layout, and enter/exit transitions. Use CSS transitions for simple effects when lighter. Do not add animation merely for decoration or stack multiple animation frameworks without a concrete reason.

### Icon rule

Do not use emoji characters as UI icons. Do not introduce Lucide/lucide-react for new UI icons. Prefer one deliberate icon family such as Phosphor, Radix Icons, Heroicons, Tabler, or a project-specific/custom SVG system.

Treat the anti-vibecoding list as anti-defaults, not absolute bans. Preserve intentional design choices that have a product-specific reason.

Arguments: $ARGUMENTS
