# Production Pup: Design Quality, UI Correctness, and Micro-Interactions

This reference extends the Design System and Anti-Vibe-Coding rules in `SKILL.md`.

The goal is not to add animation for decoration. The goal is to make interfaces feel deliberate, readable, spatially correct, tactile, and genuinely designed.

## 1. Button Contrast Is a Hard Requirement

Never ship a button whose label and background are visually indistinguishable or too close in contrast.

For every button and button-like control, verify:

- text/icon color is clearly readable against the button background
- primary, secondary, ghost, destructive, disabled, hover, active, and focus states remain distinguishable
- icons do not disappear against the background
- text does not inherit an unintended color from a parent
- hover/active styles do not reduce text contrast
- disabled styling remains understandable without becoming unreadable
- dark/light theme variants, when present, are checked independently

Do not rely on visual intuition alone when a color combination is borderline. Use a contrast checker or browser accessibility tooling where appropriate.

Prefer explicit button tokens such as `--button-bg`, `--button-fg`, `--button-border`, `--button-hover-bg`, and `--button-hover-fg` instead of unrelated one-off colors.

## 2. Button Overlap and Hit-Target Integrity

Buttons must never visually or interactively overlap unless the overlap is an intentional, documented composition.

Common AI-generated failures include:

- two adjacent buttons partially covering each other
- one button sitting on top of another because of absolute positioning
- hover styles revealing a hidden second button underneath
- transparent button backgrounds exposing another clickable control
- negative margins causing hit targets to collide
- flex items shrinking until labels or controls overlap
- z-index fixes hiding the underlying layout bug
- two controls occupying the same pointer area

For groups of buttons:

- use flex/grid with explicit `gap`
- allow wrapping where the available width can become constrained
- use sensible `min-width: 0` and max-width rules
- make text fit or wrap intentionally
- avoid absolute positioning for normal CTA/button groups
- verify the actual clickable rectangles, not just the static screenshot
- test hover, focus, keyboard tab order, and touch interaction
- verify that one control cannot intercept clicks intended for another

If two controls belong side-by-side, their hit areas must be distinct at every tested breakpoint.

Test button groups at narrow mobile widths as well as desktop widths.

## 3. Layout Collision Audit

Do a dedicated collision pass after the page is visually complete.

Inspect:

- buttons and links
- navigation items
- badges and labels
- icons beside text
- cards touching each other
- floating controls
- sticky headers
- modals and dialogs
- dropdowns
- tooltips
- form fields
- images and text
- absolute-positioned decorative elements
- responsive breakpoint transitions

Check both visual overlap and pointer-event overlap.

Do not declare a layout correct merely because it looks fine at one viewport.

## 4. Real Micro-Interactions

A polished interface should communicate state changes clearly.

Use subtle micro-interactions for meaningful events such as:

- button hover and press
- focus
- navigation transitions
- menu open/close
- accordion open/close
- tab changes
- filter changes
- copy-to-clipboard success
- form validation
- loading completion
- toast appearance/disappearance
- modal enter/exit
- list/item insertion or removal
- route/page transitions when appropriate
- scroll-triggered reveal of important content

The interaction should reinforce what happened. Do not animate every element just because it can move.

## 5. Motion.dev and Animation Libraries

For React projects, prefer **Motion** (`motion`, imported from `motion/react`) for purposeful UI micro-interactions when the project can reasonably support it. Motion supports hover, tap, focus, in-view, layout, enter/exit, and gesture animation patterns. citeturn1search0turn1search1

Typical uses:

- `whileHover` for restrained hover feedback
- `whileTap` for press feedback
- `whileFocus` for accessible focus animation where useful
- `whileInView` for restrained section reveals
- `AnimatePresence` for enter/exit transitions
- `layout` for genuine layout changes
- variants for coordinated but controlled sequences

Use CSS transitions for simple isolated effects when that is lighter and clearer. Do not add Motion merely to make a dependency list look impressive.

Motion's current React installation uses the `motion` package and imports from `motion/react`. citeturn1search4

Other animation libraries may be used when they solve a real problem, but do not stack multiple animation frameworks without justification.

## 6. Motion Quality Rules

Good motion should be:

- subtle
- fast enough to feel responsive
- consistent across the product
- interruptible when appropriate
- tied to user intent or state
- performant
- accessible

Prefer animating `transform` and `opacity` when possible. Avoid animation that repeatedly forces expensive layout or paint work. Motion's documentation specifically recommends compositor-friendly properties such as transform and opacity for best performance. citeturn1search2

Avoid:

- constant floating UI
- endless looping animations without purpose
- excessive parallax
- bouncing buttons
- large scale jumps
- dramatic page transitions for ordinary navigation
- animation on every card
- random stagger effects
- cursor-following decoration unless the product genuinely benefits from it
- animation that delays a user's ability to interact

## 7. Reduced Motion

Respect `prefers-reduced-motion`.

For non-essential motion:

- reduce distance and duration
- remove parallax
- remove decorative loops
- preserve the underlying state change
- keep the interface understandable without animation

Do not make critical information available only through animation.

## 8. Icons: No Emoji UI

Do not use emoji characters as interface icons.

For example, avoid using characters such as `🚀`, `✨`, `⚙️`, `🔥`, `❤️`, `→`, or random emoji symbols as replacements for real UI icons.

Use a proper icon library or project-specific SVG icons instead.

**Do not use Lucide / lucide-react for new UI icons in this skill.** It is too common in generated interfaces and often contributes to a generic AI-generated visual language.

Prefer an icon system with a deliberate visual identity, such as:

- Phosphor Icons
- Radix Icons
- Heroicons
- Tabler Icons
- an existing project-specific icon set
- custom SVG icons when the product needs a distinctive symbol

Do not mix multiple icon families without a reason.

Choose one family whose stroke/fill, optical weight, corner treatment, and sizing fit the design system.

## 9. Icon Implementation Rules

Icons should:

- have consistent visual weight
- use accessible labels when they are the only content of a control
- have correct `aria-hidden` behavior when decorative
- align optically with adjacent text
- use consistent sizes
- have enough touch target around them
- not be used merely as decoration everywhere

A button containing only an icon must have an accessible name.

Do not replace meaningful text with an icon if the icon is ambiguous.

## 10. Premium Feel Comes From Restraint

A website does not feel premium because it has many animations.

Premium feel comes from a combination of:

- correct spacing
- strong typography
- clear hierarchy
- readable contrast
- precise alignment
- distinct interaction states
- intentional iconography
- smooth but restrained motion
- correct loading/success/error feedback
- absence of visual collisions
- consistent timing and easing
- responsive behavior that feels designed rather than compressed

The micro-interactions should make the interface feel alive without making the interface perform a show.

## 11. Interaction State Matrix

For important interactive controls, inspect:

| State | Must be considered |
| --- | --- |
| Rest | readable, correctly positioned, obvious action |
| Hover | subtle feedback, no collision, no contrast failure |
| Focus | visible keyboard focus, no layout jump |
| Active/Pressed | clear physical/state feedback |
| Disabled | clearly unavailable without becoming unreadable |
| Loading | prevents confusing duplicate actions where needed |
| Success | confirms the intended result |
| Error | explains failure and provides a next action |

Not every control needs every state, but every state that exists must be intentionally designed.

## 12. Final Visual Interaction Test

Before declaring the design complete:

1. View every important page at desktop width.
2. View the same pages at narrow mobile widths.
3. Hover every major interactive control.
4. Tab through the interface.
5. Click every primary and secondary CTA.
6. Test buttons beside other buttons.
7. Test menus, dropdowns, modals, and overlays.
8. Look for hidden controls underneath visible controls.
9. Check that hover states do not reveal overlapping elements.
10. Check that text and icons remain readable in every state.
11. Test reduced-motion behavior.
12. Check the browser console for UI/runtime errors.

If a control looks correct but another control becomes visible or clickable underneath it during hover/focus/active states, treat that as a layout bug and fix the underlying structure rather than adding another z-index.
