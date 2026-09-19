# UI Vocabulary Reference

Use precise UI vocabulary when auditing, discussing, or modifying websites and web apps. The goal is not jargon for its own sake. Precise terms make visual requirements, implementation tasks, and verification criteria unambiguous.

## 1. Page Structure & Layout

- **Hero section**: Main introductory area of a page.
- **Navbar**: Main navigation area.
- **Header**: Top area containing branding and/or navigation.
- **Footer**: Bottom section of a website.
- **Container**: Maximum-width wrapper around content.
- **Section**: Distinct horizontal area of a page.
- **Split layout**: Layout divided into two major areas.
- **Grid layout**: Elements arranged in rows and columns.
- **Flex layout**: Elements arranged along an axis.
- **Full-bleed**: Content extending to viewport edges.
- **Sidebar**: Secondary vertical content area.
- **Rail**: Narrow side area for supporting content.
- **Content wrapper**: Wrapper controlling content positioning.
- **Breakpoint**: Screen width where layout behavior changes.

When reporting layout problems, prefer the specific term and the observed behavior: for example, "the content wrapper is too wide at the tablet breakpoint" instead of "the layout feels off."

## 2. Common Components

- **Card**: Contained block of related content.
- **CTA**: Element encouraging an action.
- **Badge**: Small status or category label.
- **Chip**: Compact tag or filter element.
- **Pill**: Highly rounded compact element.
- **Avatar**: User/profile representation.
- **Icon button**: Button represented primarily by an icon.
- **FAB**: Floating Action Button.
- **Divider**: Visual separator between content.
- **Breadcrumbs**: Hierarchical page navigation.
- **Tabs**: Controls for switching between related content views.
- **Accordion**: Expand/collapse content control.
- **Dropdown**: Menu revealing additional options.
- **Select**: Form control for choosing an option.

Do not assume a component needs to exist just because it is common. Use the product's actual information architecture and interaction needs.

## 3. Popups, Floating UI & Overlays

- **Modal**: Large popup requiring attention.
- **Dialog**: Focused interaction window, especially for a specific task or confirmation.
- **Popover**: Small contextual floating panel.
- **Tooltip**: Small explanatory popup.
- **Drawer**: Panel sliding from a side.
- **Bottom sheet**: Panel sliding upward from the bottom.
- **Overlay**: Layer placed over another element.
- **Backdrop**: Background layer behind a modal/dialog.
- **Toast**: Temporary notification.
- **Context menu**: Menu based on a selected item or interaction.

Audit these for focus management, dismissal behavior, stacking, hit areas, responsive behavior, keyboard access, and accidental interaction with content behind them.

## 4. Loading, Empty, Error & Success States

These states are easy for AI-generated products to omit and should be explicitly audited when async or stateful behavior exists.

- **Skeleton loader**: Placeholder while content loads.
- **Spinner**: Animated loading indicator.
- **Progress bar**: Shows task completion.
- **Loading state**: UI while an operation is processing.
- **Empty state**: UI when there is no data or content.
- **Error state**: UI when an operation fails.
- **Success state**: UI after successful completion.
- **Disabled state**: Element unavailable for interaction.

For each relevant async flow, verify the correct state exists and that state changes communicate what happened without trapping the user.

## 5. Interaction States

- **Hover state**: Appearance when a pointer is over an element.
- **Focus state**: Appearance when an element receives keyboard or programmatic focus.
- **Active state**: Appearance while an element is being interacted with.
- **Selected state**: Appearance when an option is selected.
- **Pressed state**: Feedback while clicking/tapping.
- **Disabled state**: Appearance when unavailable.
- **Transition**: Visual change between states.

Every interactive control should have appropriate states for its interaction model. Do not add decorative hover effects where they do not communicate state or improve usability.

## 6. Responsive & Mobile Vocabulary

- **Responsive layout**: Layout adapting to screen size.
- **Mobile-first**: Designing from the smallest relevant viewport upward.
- **Breakpoint**: Point where layout behavior changes.
- **Safe area**: Protected mobile screen region.
- **Bottom navigation**: Navigation fixed near the screen bottom.
- **Swipe gesture**: Finger movement interaction.
- **Pull-to-refresh**: Drag-down gesture to refresh content.
- **Touch target**: Interactive area sized for touch.

Verify behavior at actual breakpoints rather than assuming a CSS framework's defaults are sufficient. Check wrapping, overflow, safe areas, fixed navigation, dialogs, drawers, and touch targets.

## 7. Animation & Motion

- **Marquee**: Continuously scrolling content.
- **Fade**: Gradual appearance/disappearance.
- **Slide animation**: Element moving into position.
- **Scale animation**: Element growing/shrinking.
- **Easing**: Controls animation acceleration/deceleration.
- **Stagger**: Elements animate one after another.
- **Parallax**: Layers move at different speeds.
- **Reveal animation**: Content appears as it enters view.
- **Microinteraction**: Tiny interaction feedback.
- **Scroll-linked animation**: Animation tied to scroll position.

Motion must have a purpose. Prefer transform/opacity for performant effects, respect reduced-motion preferences, and avoid animation that obscures content, delays interaction, or becomes repetitive decoration.

## 8. Typography & Visual Hierarchy

- **Typography scale**: Structured range of font sizes.
- **Font weight**: Thickness of text.
- **Line height**: Vertical spacing between text lines.
- **Letter spacing**: Space between characters.
- **Text hierarchy**: Importance conveyed through text styling.
- **Display type**: Large expressive typography.
- **Body copy**: Main explanatory text.
- **Text contrast**: Difference between text and its background.

Use these terms when diagnosing hierarchy and readability instead of vague descriptions such as "make the text pop."

## 9. Spacing & Visual Polish

- **Whitespace**: Empty visual space.
- **Padding**: Space inside an element.
- **Margin**: Space outside an element.
- **Gap**: Space between flex/grid children.
- **Alignment**: How elements line up.
- **Consistency**: Repeating visual rules.
- **Density**: How much information is packed together.
- **Rhythm**: Repeating spacing and size relationships.

Audit spacing as a system. Look for inconsistent gaps, accidental margins, cramped touch targets, uneven alignment, and broken rhythm across responsive states.

## 10. Visual Styling

- **Border radius**: Corner rounding.
- **Border**: Edge around an element.
- **Box shadow**: Shadow around an element.
- **Elevation**: Visual sense of depth.
- **Opacity**: Transparency level.
- **Gradient**: Gradual color transition.
- **Blur**: Softening visual detail.
- **Backdrop blur**: Blurring whatever is behind an element.
- **Overlay**: Layer placed over content.
- **z-index**: Stacking order.

Do not use z-index as a substitute for fixing incorrect positioning, stacking contexts, overflow, or DOM structure. Audit the underlying layout when elements collide.

## 11. Forms & Inputs

- **Input field**: Field where users enter data.
- **Textarea**: Multi-line text input.
- **Checkbox**: Multiple-selection control.
- **Radio button**: Single-choice control.
- **Toggle/switch**: On/off control.
- **Label**: Text describing a form control.
- **Helper text**: Supporting guidance below an input.
- **Validation state**: Visual response to input validity.
- **Inline validation**: Validation shown directly beside or near the field.

Audit labels, instructions, focus, validation timing, error recovery, disabled/loading states, keyboard behavior, and mobile touch targets.

## 12. Dashboards & Product UI

- **Metric card**: Highlights an important number.
- **Data table**: Structured rows and columns.
- **Filter bar**: Controls for narrowing results.
- **Status indicator**: Communicates state.
- **Progress indicator**: Shows progress.
- **Activity feed**: Chronological list of events.
- **KPI**: Key performance indicator.
- **Command palette**: Keyboard-driven action/search UI.
- **Data visualization**: Graphical representation of data.

For product UI, verify that terminology matches the actual information architecture and that dense interfaces remain usable on smaller screens.

## 13. Design-System Vocabulary

- **Design system**: Reusable design rules and components.
- **Component**: Reusable UI building block.
- **Variant**: Different version of a component.
- **Design token**: Reusable design value.
- **Theme**: Overall visual configuration.
- **Component library**: Collection of reusable components.
- **Utility class**: Reusable styling rule.
- **Global style**: Styling applied across the application.

Prefer existing project conventions. Do not introduce a second component system, token system, or styling approach without a concrete reason.

## 14. High-Value AI/Vibe-Coding Terms

- **Responsive**: Adapts to different screens.
- **Reusable component**: Component designed for repeated use.
- **Variant**: Different state/version of a component.
- **Refactor**: Restructure code without changing intended behavior.
- **Extract**: Move reusable logic or UI into its own unit.
- **Conditional rendering**: Showing UI based on conditions.
- **State**: Current condition of an interface.
- **Interaction**: User action and resulting behavior.
- **Accessibility / a11y**: Making the UI usable for more people.
- **Semantic HTML**: Using elements according to their meaning.

Use precise vocabulary in prompts, findings, fixes, and verification steps. A request such as "make this premium" is underspecified. A better request identifies the actual changes, for example: "Reduce the container width, increase whitespace, strengthen text hierarchy, soften elevation, and add a subtle hover transition."

## Production Pup Usage

When auditing or fixing a product:

1. Name the exact UI structure or component involved.
2. Name the state or responsive condition involved.
3. Describe the observed behavior.
4. State the intended behavior.
5. Apply the smallest safe implementation change.
6. Verify the result at the affected viewport and interaction state.

Example:

> "At the tablet breakpoint, the right rail collides with the content wrapper. Stack the rail below the primary content at that breakpoint and verify there is no horizontal overflow."

Do not turn this vocabulary into a requirement to use every component or visual effect. The vocabulary exists to make design and engineering communication precise.
