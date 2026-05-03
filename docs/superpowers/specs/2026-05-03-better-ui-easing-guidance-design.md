# Better UI Easing Guidance Design

## Goal

Improve `skills/better-ui` so it can guide easing choice with more nuance without turning into an animation catalog.

The new guidance should help answer:

- when the current default categories are enough
- when a more specific easing family is useful
- which families fit common UI motion goals
- which families should be used sparingly or avoided by default

## Problem

The current animation reference is intentionally compact and strong on first-order rules:

- entering UI: `ease-out`
- moving or morphing on screen: `ease-in-out`
- hover or color changes: `ease`
- constant motion: `linear`

That is good default guidance, but it does not help much when a designer or implementer wants a slightly more specific motion tone such as:

- softer and quieter
- more standard and stable
- heavier and weightier
- more expressive with overshoot

If we add a full easing taxonomy directly, the skill risks encouraging animation-first thinking and unnecessary motion complexity.

## Recommended approach

Keep the existing first-order guidance unchanged, then add a second-order section in `references/animations.md` for choosing an easing family only after the interaction type is already clear.

This keeps the skill aligned with its current stance:

- motion is optional
- responsiveness matters more than flourish
- most UI should use simple, predictable curves

## Content shape

### 1. Keep the current primary guidance

Do not replace the current interaction mapping. It should remain the default decision layer.

### 2. Add an `Easing families` section

This section should explain that easing families are for tone selection, not for deciding whether animation belongs in the interaction.

Recommended grouping:

- `sine`, `quad`
  For subtle, low-distraction motion such as hover, fade, and very light UI movement.
- `cubic`, `quart`
  For standard interface transitions such as popovers, modals, drawers, and panel motion.
- `quint`, `expo`, `circ`
  For stronger emphasis, larger elements, or motion that should feel weightier or more dramatic.
- `back`, `anticipate`
  For expressive special cases only, such as a toast, celebratory state, or a deliberate characterful motion.

### 3. Add a `Use sparingly` section

This section should protect the skill from overuse and style drift.

It should explicitly call out:

- `ease-in`
  Avoid for ordinary UI entry or response.
- `back`
  Use only for intentional emphasis, not routine interface motion.
- `anticipate`
  Use only where the slight reverse motion helps communication instead of adding friction.
- `jump`
  Niche, style-driven, and usually wrong for general product UI.

## Curve examples

Include a small token set rather than every candidate curve.

Recommended examples:

- `--ease-soft-out`
- `--ease-standard-out`
- `--ease-strong-out`
- `--ease-heavy-out`
- `--ease-expressive-out`

These should map approximately to:

- soft: `sine` or `quad`
- standard: `cubic`
- strong: `quart` or `quint`
- heavy: `circ`
- expressive: `back`

Keep `ease-in-out` examples available for on-screen movement, but avoid turning the file into a full easing library.

## Proposed file changes

### `skills/better-ui/references/animations.md`

Add:

- a short `Easing families` section after the current easing rules
- a compact table mapping interaction goals to easing families
- a short `Use sparingly` section
- a minimal curve token example set

### `skills/better-ui/SKILL.md`

Make a small wording change in the animation gate so the top-level skill points readers to the new easing-family guidance only when the default categories are not enough.

## Non-goals

- do not add a full encyclopedia of easing families
- do not encourage motion where no motion is better
- do not normalize `back`, `anticipate`, or `jump` as everyday defaults
- do not weaken the current guidance against ordinary `ease-in`

## Testing and review

This is a documentation and guidance change, so validation is editorial rather than runtime.

Review criteria:

- the default decision path still starts with restraint
- the new content helps choose tone without increasing complexity
- expressive families are clearly treated as exceptions
- the main skill stays short and the detail lives in the reference file

## Open decisions resolved

- Include easing families: yes
- Include the full original taxonomy verbatim: no
- Keep `jump`: mention only as a niche or avoid-by-default case
- Preserve anti-`ease-in` guidance: yes
