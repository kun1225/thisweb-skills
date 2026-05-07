# Typography

Typography polish is mostly about removing tiny sources of friction: awkward line breaks, heavy rendering, and shifting numerals.

## UX laws for readable UI

- **Cognitive Load**: every extra label, line break, and visual treatment costs attention. Remove text that repeats structure the UI already communicates.
- **Chunking**: group text into meaningful units before adjusting font size or color. Short headings, compact labels, and grouped fields reduce parsing effort.
- **Serial Position Effect**: users remember the first and last items in a sequence more easily. Put the most important list items, tabs, or steps where attention naturally lands.

## Responsive type

Prefer `clamp()` for headings that need fluid size changes across available space. Use viewport or breakpoint changes more cautiously for body and description text so reading rhythm stays stable.

## Leading

Chinese text usually reads best with `line-height` around `1.2em` to `1.5em`. Use the tighter end for compact UI labels and the looser end for longer reading blocks.

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
