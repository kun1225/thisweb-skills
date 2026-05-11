# Design To Code

After analyzing the reference image, implement in a copy-oriented way.

The goal is not "inspired by the image."
The goal is "visually faithful to the image, translated into real frontend."

## Design-to-code discipline

During implementation:

- follow the reference closely
- preserve layout logic
- preserve spacing rhythm
- preserve section ordering
- preserve text and image balance
- preserve typography mood
- preserve component style
- preserve overall visual cleanliness

Do not drift into a different design direction during implementation.

## Anti-drift implementation rules

A common failure mode is design drift: the source image looks strong, but the coded result becomes generic.

Strictly avoid:

- simplifying into default templates
- replacing distinctive sections with generic rows
- compressing generous spacing into dense layout
- replacing strong typography with plain hierarchy
- removing the page's visual identity for convenience
- merging section logic into repetitive patterns that were not present in the source image
- reintroducing nested-box complexity that should have been avoided

The final coded result should still feel like the same design as the reference.

## Resolving missing detail

When the image leaves something ambiguous, resolve it in this order:

1. preserve the visible design language
2. preserve layout and spacing logic
3. preserve component family
4. preserve mood and polish level
5. choose the most implementation-friendly faithful version only after the steps above

Do not fill ambiguity with generic defaults too quickly.

## Implementation stance

Use the extracted analysis as the basis for code decisions.

If the image shows a strong idea clearly, keep it.
If the image leaves a detail unclear, make the smallest faithful inference.

The code is a translation layer, not a redesign pass.
