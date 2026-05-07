# Layout

Layout polish starts with structure. Before changing color, shadows, or motion, check whether the UI already groups related content, separates unrelated content, and lets the eye find the next useful action quickly.

## Diagnose the layout

Ask these questions before editing:

- Can you identify the primary element, secondary element, and major groups with a quick squint test?
- Are related elements close together, or are they separated by decorative whitespace?
- Are unrelated groups separated clearly, or does everything sit at the same distance?
- Is the page using boundaries because the content needs containment, or because the layout lacks hierarchy?
- Does the density match the job? Repeated work and comparison need tighter layouts than marketing or onboarding surfaces.
- Does the structure adapt on smaller screens, or does it only shrink?

## Use a spacing system

Use values from the project's existing spacing scale. If the project has no clear scale, create a small one and stick to it.

Rules:

- Use `gap` for sibling spacing before reaching for one-off margins.
- Keep related elements tight, usually 8-12px apart.
- Separate distinct groups more generously, usually 32-96px depending on page density.
- Avoid equal spacing everywhere. Repetition without contrast makes hierarchy disappear.
- Use `clamp()` for page-level spacing that should breathe on larger screens.

For page edges, keep one baseline edge token even if sections use different internal spacing or content widths:

```css
:root {
  --spacing-contain-max: 1600px;
  --spacing-edge: max(
    max(min(3.5vw, 96px), 8px),
    calc((100vw - var(--spacing-contain-max)) / 2)
  );
}
```

Use `padding-inline: var(--spacing-edge)` as the default page-edge constraint. This keeps edge spacing fluid, caps the effective content width on very large screens, and avoids the width mismatches that `margin-inline` can introduce when scrollbars appear. Prefer `px-edge` over `mx-edge` for page containment.

```css
.section {
  padding-block: clamp(48px, 8vw, 96px);
  padding-inline: var(--spacing-edge);
}

.stack {
  display: flex;
  flex-direction: column;
  gap: 12px;
}
```

## Choose structure before decoration

Start with the lightest structure that communicates the relationship.

Use spacing when content belongs together naturally. Use dividers when the user needs to compare rows or scan a list. Use sections when content changes topic. If an item needs a visual boundary, apply the card decision order in `surfaces.md`.

Avoid turning page sections into floating cards. A page can feel designed through alignment, spacing, and typography without every region becoming a bordered box.

## UX laws for layout

Use these laws as practical checks, not as decoration for a rationale.

- **Law of Proximity**: related elements should sit close together. Increase distance between unrelated groups before adding visual containers.
- **Law of Common Region**: a shared boundary makes elements feel grouped. Use it when proximity is not enough, but avoid boxed regions when spacing already communicates the group.
- **Law of Similarity**: repeated objects with the same role should share structure, alignment, and interaction treatment. Break similarity only to signal a real difference.
- **Hick's Law**: decision time rises with the number and complexity of choices. Group choices, hide advanced controls until needed, and avoid presenting every action at the same priority.
- **Jakob's Law**: common workflows should follow familiar patterns. Reserve unusual layouts for places where the product gains real clarity or speed.

## Pick the right layout tool

Use Flexbox for one-dimensional layouts:

- nav bars
- button groups
- inline controls
- card internals
- stacked content
- simple wrapping rows

Use Grid for two-dimensional layouts:

- dashboards
- page shells
- bento or editorial arrangements
- dense comparison views
- layouts where rows and columns need coordinated control

Do not default to Grid when `flex-wrap` handles the layout cleanly.

```css
.responsive-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 24px;
}
```

## Preserve scanability

Scanability usually beats symmetry.

Rules:

- Prefer stable left edges for lists, forms, settings, and dashboards.
- Keep labels close to the values or controls they describe.
- Align repeated actions predictably.
- Put numeric columns in a consistent alignment and use tabular numbers where values update or compare.
- Avoid centered stacks for dense product UI unless the content is truly short and singular.
- Vary repeated sections so the page does not become an identical card grid.

## Make density intentional

Density should follow usage frequency and information type.

Use tighter density for:

- tables
- admin screens
- settings
- monitoring
- repeated workflows
- comparison-heavy views

Use more breathing room for:

- onboarding
- empty states
- editorial content
- marketing sections
- destructive confirmations

When a layout feels cramped, increase group separation before increasing every padding value. When it feels sparse, tighten related elements before shrinking the whole page.

## Responsive behavior

Responsive layout should change structure, not only size.

Use viewport queries for page-level layout. Use container queries for components whose available width changes independently from the viewport, especially inside layouts with sidebars, split panes, or resizable panels. This lets the same card stay compact in a narrow sidebar and expand in the main content area without viewport-specific hacks.

Check:

- Sidebars collapse or become drawers when space is constrained.
- Toolbars wrap into grouped controls instead of overflowing.
- Tables switch to a readable narrow-screen pattern only when columns can no longer compare well.
- Components adapt to their container when sidebar or panel width changes independently from the viewport.
- Fixed-format elements use stable dimensions with `aspect-ratio`, `minmax()`, or explicit min/max constraints.
- Text does not overlap controls or force controls to resize during hover, loading, or state changes.

## Never

- Use arbitrary spacing values when a scale exists.
- Make all padding and gaps identical.
- Add boundaries because spacing is weak.
- Repeat the same card formula everywhere: icon, heading, text; or badge, heading, subheading, description.
- Add badges or subtitles when the title and body already communicate the hierarchy.
- Center everything by default.
- Use decorative containers for full page sections.
- Animate layout properties such as `width`, `height`, `padding`, or `margin` for ordinary UI motion.
- Let hover, loading, or label changes resize fixed-format controls.

## Review checks

- The primary action or content is obvious within two seconds.
- Related items feel grouped without needing extra boxes.
- Distinct groups have enough separation to read as separate ideas.
- The layout remains scannable on mobile and desktop.
- Density matches the user's workflow.
- The structure still works with long labels, dynamic numbers, loading states, and empty states.
