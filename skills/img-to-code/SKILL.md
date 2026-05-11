---
name: img-to-code
description: Turn pasted UI images, screenshots, or mockups into real frontend code while respecting BRAND.md and DESIGN.md. Use this whenever the user shares a visual reference and wants it recreated faithfully in code, adapted to the project's brand voice, design tokens, and component rules rather than copied blindly.
---

# Image To Code

Use this skill when the user already has an image-based UI reference and wants code derived from it inside a real project with its own brand and design rules.

This skill is for:

- screenshots of websites or apps
- mockups
- generated UI references
- design crops focused on specific sections
- cases where visual fidelity matters

This skill is not for:

- bug fixes with no image reference
- abstract UI brainstorming with no visual source
- tasks that mainly need image generation rules

## Core stance

This is a constrained translation task, not a blind copy task.

Do not jump straight into coding from vibes.
Do not flatten a strong design into generic frontend defaults.
Do not treat the image as the only authority when the project already has `BRAND.md`, `DESIGN.md`, tokens, or reusable components.

First understand the project constraints.
Then analyze the image carefully.
Then implement from that analysis using the project's system.

## Source priority

Treat the implementation as the result of three inputs:

1. `BRAND.md` for audience, positioning, tone, and copy constraints
2. `DESIGN.md` for color tokens, type tokens, spacing rules, motion, component style, and banned patterns
3. the image for composition, hierarchy, spacing rhythm, and visual detail

Use the image to understand what should be built.
Use `BRAND.md` to decide how it should speak.
Use `DESIGN.md` to decide how it should be expressed in the project's design language.

If the image conflicts with the brand or design system, preserve the image's intent and structure while translating it into project-approved tokens and patterns.

## Required workflow

1. Read project `BRAND.md` if present. If the project does not provide one, read [../web-brand-md/references/BRAND.md](../web-brand-md/references/BRAND.md) as the expected structure.
2. Read project `DESIGN.md` if present. If the project does not provide one, read [../design-md/references/DESIGN.md](../design-md/references/DESIGN.md) as the expected structure.
3. Read [references/image-analysis.md](references/image-analysis.md).
4. Inspect the provided image or images systematically.
5. Split findings into three buckets before coding:
   - what must be preserved from the image
   - what must be adapted to fit `BRAND.md` and `DESIGN.md`
   - what is ambiguous or missing
6. Read [references/design-to-code.md](references/design-to-code.md).
7. Implement the UI using project tokens, components, and layout patterns wherever they can express the reference faithfully.
8. Render the result and compare it against the image for hierarchy, spacing, typography, and overall feel.
9. Fix visible mismatches before considering the task complete.
10. Invent missing details only after preserving the visible design language and respecting brand and design-system constraints.

## Adaptation rules

When the image conflicts with `DESIGN.md`:

- preserve structure, hierarchy, and rhythm from the image
- translate literal colors, typography, radius, shadows, and motion into the project's tokens and component rules
- keep the same visual intent without copying banned implementation patterns

When the image text conflicts with `BRAND.md`:

- preserve the information architecture and emphasis from the image
- rewrite copy to fit the brand voice, audience, and product framing
- avoid placeholder marketing language that weakens the original layout

When the project already has reusable UI primitives:

- prefer extending or composing them over introducing one-off styling
- only create custom styling when existing primitives cannot reproduce the reference faithfully

## Ambiguity handling

Not all ambiguity is equal.

Minor ambiguity can be resolved with the smallest faithful inference.
Examples: an approximate shadow, a slightly unclear radius, a likely spacing value.

Critical ambiguity should be surfaced before implementation or clearly called out during implementation.
Examples: unreadable hero copy, missing mobile layout, hidden interaction states, cropped navigation, or a color relationship that would conflict with `DESIGN.md`.

Do not hallucinate key content or structure just to keep momentum.

## Reference files

- [references/image-analysis.md](references/image-analysis.md) for how to analyze images cleanly and extract implementation-relevant detail
- [references/design-to-code.md](references/design-to-code.md) for how to translate the extracted design into faithful frontend code
