# Typography

Typography polish is mostly about removing tiny sources of friction: awkward line breaks, heavy rendering, and shifting numerals.

## Text wrapping

### Use `text-wrap: balance` on centered headings

Use balanced wrapping for short, centered headings and titles so line lengths feel intentional instead of leaving a single orphaned word. This is the main place where `text-balance` usually pays off.

```css
h1,
h2,
h3 {
  text-wrap: balance;
}
```

Use it on short text blocks only. Browser implementations cap how many lines they will balance. For non-centered headings, apply it only when the default wrap clearly looks awkward.

Tailwind: `text-balance`

### Use `text-wrap: pretty` as the default for general text

For most other text, default to `text-pretty`. Use it for descriptions, captions, list items, body copy, and general UI text where you want fewer awkward last lines without forcing equal line lengths.

```css
p,
li,
figcaption,
blockquote {
  text-wrap: pretty;
}
```

Tailwind: `text-pretty`

### When not to use either

Skip both on long-form text, code blocks, and preformatted content. Default wrapping is fine there.

## Font smoothing

On macOS, text can render heavier than intended. Apply smoothing at the root layout, not ad hoc on individual elements.

```css
html {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```

Tailwind root class: `antialiased`

## Tabular numbers

Use `font-variant-numeric: tabular-nums` anywhere numbers update dynamically so digits do not change width and cause layout shift.

```css
.metric {
  font-variant-numeric: tabular-nums;
}
```

```tsx
<span className="tabular-nums">{count}</span>
```

Use it for counters, timers, prices, scoreboards, and numeric table columns. Skip it for decorative numerals or identifiers where proportional spacing reads better.
