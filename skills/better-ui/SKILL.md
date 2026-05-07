---
name: better-ui
description: Improve interface quality with design engineering judgment and concrete UI polish rules. Use this whenever the user wants to make a UI feel better, polish frontend details, review visual quality, refine animations, improve hover/press states, fix typography, tune shadows/borders/radius/alignment, reduce visual awkwardness, or when an interface "feels off" even if the user does not ask for a design review explicitly.
---

# Better UI

Use this skill to move an interface from merely functional to polished, intentional, and pleasant to use. Combine taste-level judgment with concrete implementation rules. Favor changes that compound: small details, correct defaults, and motion that supports the product instead of calling attention to itself.

## Core stance

- Taste is trained. Study what feels right, then apply the same standard to the current UI.
- Small unseen details compound into a noticeable product advantage.
- Beauty is leverage. Good defaults, good timing, and good interaction design matter.
- Do not add motion or decoration by reflex. Every change should improve clarity, responsiveness, or perceived quality.
- Do not default to cards for every chunk of content. Start with spacing, typography, alignment, and dividers before introducing boxed surfaces.
- Layout comes before surface treatment. Fix grouping, rhythm, density, and scanability before adding borders, shadows, or containers.

## When to use this skill

Use it for any of these situations:

- The user asks to polish a UI, make it feel better, or improve visual quality.
- A component works but feels awkward, cheap, flat, or slightly off.
- You are building or reviewing buttons, cards, menus, drawers, popovers, tooltips, tabs, lists, dashboards, settings pages, or marketing UI.
- You are changing typography, shadows, borders, radii, spacing, alignment, icon states, image treatment, or hit areas.
- You need to decide between cards, lists, tables, sections, or dividers for presenting content.
- You are implementing or reviewing hover states, press feedback, enter/exit transitions, icon swaps, staggered reveals, drag interactions, or perceived performance.

## Working mode

Choose the mode that matches the task:

1. Build
   Apply the rules directly while keeping the product's existing visual language coherent.

2. Review
   Identify where the current UI loses quality, responsiveness, or cohesion. Prioritize the highest-leverage fixes.

3. Tune
   Keep the structure, but tighten the details: spacing, typography, shadows, motion, and interaction feedback.

## Reusable component principles

When the task involves a reusable component or UI primitive, keep these principles in scope:

- Developer experience matters. The component should be easy to adopt.
- Good defaults matter more than a long options list.
- Naming and cohesion shape how the component is perceived.
- Handle edge cases invisibly so users never notice the workaround.
- Documentation and demos are part of the product, not an afterthought.

## Animation gate

Before adding animation, answer these in order:

1. Should this animate at all?
   High-frequency interactions often feel better with no animation or much less animation.

2. What purpose does the animation serve?
   Valid reasons include feedback, state change, spatial continuity, explanation, and preventing jarring changes.

3. What easing and duration fit the interaction?
   Use responsive timing and stronger custom curves when needed; avoid sluggish motion. If the standard easing categories are not enough, use the animation reference to choose a motion family without adding unnecessary flourish.

4. Will this still feel good under repeated use?
   Keyboard-triggered or highly repetitive interactions should usually be instant.

Read [references/animations.md](references/animations.md) for the full framework and concrete implementation rules.

## Reference guide

Read only the relevant reference files for the task:

- [references/typography.md](references/typography.md) for text wrapping, font smoothing, and tabular numbers.
- [references/layout.md](references/layout.md) for spacing rhythm, hierarchy, density, responsive structure, and Flexbox vs Grid choices.
- [references/surfaces.md](references/surfaces.md) for radius, optical alignment, shadows, image outlines, hit areas, and when cards should or should not be used.
- [references/animations.md](references/animations.md) for animation decisions, easing, timing, springs, enter/exit motion, gestures, and accessibility.
- [references/performance.md](references/performance.md) for transition specificity, `will-change`, CSS vs JS motion, and performance caveats.

## Review output format

When reviewing or summarizing UI changes, group related fixes under short headings and use markdown tables with these exact columns:

| Before                  | After                                  | Why                                                   |
| ----------------------- | -------------------------------------- | ----------------------------------------------------- |
| `transition: all 300ms` | `transition: transform 160ms ease-out` | Exact properties are more predictable and feel faster |

Rules:

- Use an actual markdown table, never separate `Before:` and `After:` lines.
- Keep one row per concrete change.
- Mention the specific file or property when the snippet alone is ambiguous.
- Omit empty sections. If nothing needs changing for a principle, do not create a table for it.

## Review checklist

- Is the UI solving the problem with fewer but better details?
- Is the content grouped with spacing, typography, sections, or dividers before reaching for cards?
- Are related elements grouped tightly and unrelated groups separated clearly?
- Does the layout preserve scanability before adding surface treatment?
- Are cards only used where an item truly needs to behave as an independent interactive object?
- Are nested surfaces using correct radii and depth treatment?
- Are icons and mixed-content controls optically aligned, not just mathematically centered?
- Do interactive elements feel responsive on hover and press?
- Are enter and exit animations subtle, interruptible, and purpose-driven?
- Is repeated motion removed where instant response is better?
- Do numbers, headings, images, and small controls avoid common polish failures?
- Are performance and reduced-motion concerns handled intentionally?
