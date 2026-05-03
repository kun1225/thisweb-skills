# Surfaces

Surface polish comes from coherent radius, alignment, depth, and touch targets. Most UI that feels "off" is failing one of these basics.

## Concentric border radius

For nested rounded surfaces, the outer radius should usually equal the inner radius plus the padding between them.

```text
outerRadius = innerRadius + padding
```

```css
.card {
  border-radius: 20px;
  padding: 8px;
}

.card-inner {
  border-radius: 12px;
}
```

If the spacing between layers is large, treat them as separate surfaces instead of forcing strict concentric math.

## Optical alignment

Geometric centering is not always visual centering. Adjust until it looks balanced.

### Buttons with text and icon

The icon side often needs slightly less padding than the text side.

```css
.button-with-icon {
  padding-left: 16px;
  padding-right: 14px;
}
```

### Play triangles and asymmetric icons

Play icons, arrows, stars, and carets often look off when mathematically centered. Prefer fixing the SVG itself. If needed, make a tiny manual offset in layout.

## Shadows over borders

For cards, buttons, and containers that need depth, prefer layered transparent shadows over solid borders. Shadows adapt to varied backgrounds more naturally.

```css
:root {
  --shadow-border:
    0 0 0 1px rgba(0, 0, 0, 0.06), 0 1px 2px -1px rgba(0, 0, 0, 0.06),
    0 2px 4px 0 rgba(0, 0, 0, 0.04);
  --shadow-border-hover:
    0 0 0 1px rgba(0, 0, 0, 0.08), 0 1px 2px -1px rgba(0, 0, 0, 0.08),
    0 2px 4px 0 rgba(0, 0, 0, 0.06);
}
```

Use actual borders for dividers, table boundaries, and accessibility-critical outlines such as form controls.

## Use cards intentionally

Do not default to card components for objects such as products, articles, users, tasks, or projects.

Start with spacing, typography, alignment, and lightweight dividers first.

Use a card only when the item needs to behave as an independent interactive object, for example:

- it can be expanded or collapsed
- it can be dragged
- it can be selected
- it needs a clear visual boundary from surrounding content

Avoid cards when:

- the content is a simple text list
- the user needs to compare many rows or fields
- high information density is required
- spacing already communicates grouping clearly
- the card would only be decorative
- the page would become a stack of bordered or shadowed boxes
- cards would be nested inside other cards

## Card decision order

1. Can spacing and typography group the content clearly?
   If yes, do not use a card.

2. Is the item an independent interactive object?
   If no, use a list, table, section, or divider.

3. Does the item contain actions, mixed content, states, or a real need for visual boundary?
   If yes, a card is appropriate.

4. Will a card reduce scanability or comparison efficiency?
   If yes, use a list or table instead.

If none of those checks rule it out, a card is acceptable.

## Image outlines

Images often need a subtle outline so they sit cleanly against different surfaces.

Apply the outline to the rounded, clipping wrapper around the image, not directly to the `img`. In practice this means the element with `border-radius` and `overflow: hidden` gets the outline.

Use `outline`, not `border`, so the treatment does not affect layout.

```css
.image-frame {
  overflow: hidden;
  border-radius: 16px;
  outline: 1px solid rgba(0, 0, 0, 0.1);
  outline-offset: -1px;
}
```

Dark mode:

```css
.image-frame {
  overflow: hidden;
  border-radius: 16px;
  outline: 1px solid rgba(255, 255, 255, 0.1);
  outline-offset: -1px;
}
```

Rules:

- Light mode uses pure black at `rgba(0, 0, 0, 0.1)`.
- Dark mode uses pure white at `rgba(255, 255, 255, 0.1)`.
- Put the outline on the rounded wrapper that clips the image.
- Do not use tinted neutrals like slate or zinc for image outlines.
- Do not tint the outline to match the brand color.

Tailwind:

```tsx
<div className="overflow-hidden rounded-2xl outline outline-1 -outline-offset-1 outline-black/10 dark:outline-white/10">
  <img className="block size-full object-cover" />
</div>
```

## Minimum hit area

Interactive controls should have at least a 40x40px hit area, and ideally 44x44px when practical.

If the visible control is smaller, extend the target with a pseudo-element.

```css
.checkbox {
  position: relative;
  width: 20px;
  height: 20px;
}

.checkbox::after {
  content: "";
  position: absolute;
  top: 50%;
  left: 50%;
  width: 40px;
  height: 40px;
  transform: translate(-50%, -50%);
}
```

Never let expanded hit areas overlap neighboring interactive elements.
