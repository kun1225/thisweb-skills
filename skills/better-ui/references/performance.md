# Performance

Polished UI should stay smooth under real load, not just in an empty local demo.

## UX law for responsiveness

**Doherty Threshold**: productivity improves when users and the system interact without either side waiting on the other. Treat 400ms as the upper bound for visible feedback, then tune frequent interactions to feel closer to instant.

## Transition only what changes

Never use `transition: all` and avoid Tailwind's generic `transition` utility when you know the exact animated properties.

```css
.button {
  transition-property: transform, background-color;
  transition-duration: 150ms;
  transition-timing-function: ease-out;
}
```

Tailwind:

```tsx
<button className="transition-[scale,opacity,filter] duration-150 ease-out" />
```

`transition-transform` is fine when you are only animating transform-related properties.

## Use `will-change` sparingly

Only add `will-change` when you notice first-frame stutter and only for compositor-friendly properties.

Good candidates:

- `transform`
- `opacity`
- `filter`
- `clip-path`

Bad candidates:

- `all`
- `padding`
- `background-color`
- `width`
- `height`

Each promoted layer costs memory, so do not spray it everywhere.

## Prefer transform and opacity

Animating layout properties such as `width`, `height`, `margin`, or `padding` is much more expensive than animating `transform` and `opacity`.

## CSS variables caveat

CSS variables inherit. Updating a variable on a parent can trigger style recalculation across many descendants. For highly interactive motion, it is often cheaper to update the element's `transform` directly.

```js
element.style.transform = `translateY(${distance}px)`;
```

## CSS vs JS animation tradeoffs

CSS animations generally stay smoother under load because they can run off the main thread. Use them for predetermined motion.

JavaScript-driven animation is still appropriate for dynamic, interruptible, or stateful interactions.

## Motion caveat

Motion shorthand props such as `x`, `y`, and `scale` are convenient but not the best choice when you need maximum smoothness under heavy load. Prefer animating the full `transform` string in those cases.

```tsx
<motion.div animate={{ transform: "translateX(100px)" }} />
```

## Real-world checks

- Test under actual page load or state churn, not only static conditions.
- Slow animations down temporarily to inspect timing issues.
- Verify gestures on physical devices when touch behavior matters.
