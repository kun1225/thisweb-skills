# Animations

Animation quality comes from judgment first, implementation second. The right answer is often less motion, faster feedback, or no animation at all.

## Decision framework

Before animating, answer these questions in order.

### 1. Should this animate at all?

Judge by frequency:

| Frequency           | Recommendation                |
| ------------------- | ----------------------------- |
| 100+ times a day    | Remove animation              |
| Tens of times a day | Remove or drastically reduce  |
| Occasional          | Standard UI animation is fine |
| Rare or one-time    | Delight can be appropriate    |

Never animate keyboard-triggered actions that users repeat constantly.

### 2. What purpose does it serve?

Animation should earn its keep. Good reasons include:

- feedback
- state indication
- spatial continuity
- explanation
- softening abrupt appearance or disappearance

If the only reason is "it looks cool," that is usually not enough for frequently seen UI.

### 3. What easing should it use?

Prefer stronger custom curves over weak built-in defaults.

```css
:root {
  --ease-out: cubic-bezier(0.23, 1, 0.32, 1);
  --ease-in-out: cubic-bezier(0.77, 0, 0.175, 1);
  --ease-drawer: cubic-bezier(0.32, 0.72, 0, 1);
}
```

Guidance:

- entering UI: `ease-out`
- moving or morphing on screen: `ease-in-out`
- hover or color changes: `ease`
- constant motion: `linear`

Do not use `ease-in` for ordinary UI entry or response. It feels slow at the exact moment users are watching.

### Easing families

Use easing families to choose tone only after the interaction type is already clear. Most product UI still wants a simple, predictable curve.

| Goal                         | Family         | Typical use                                                       |
| ---------------------------- | -------------- | ----------------------------------------------------------------- |
| subtle and low-distraction   | `sine`, `quad` | hover, fade, very light slides, quiet supporting motion           |
| standard interface movement  | `cubic`, `quart` | popovers, modals, drawers, panels, ordinary UI transitions      |
| stronger emphasis            | `quint`, `expo` | larger elements, branded emphasis, dramatic but still controlled |
| heavier or weightier motion  | `circ`         | larger cards, sheets, and surfaces that should feel more massive  |
| expressive special cases     | `back`, `anticipate` | toast, celebratory states, deliberate characterful motion    |

Pick the least expressive family that achieves the result. Most interfaces should live in the `sine` to `quart` range.

Example tokens:

```css
:root {
  --ease-soft-out: cubic-bezier(0.61, 1, 0.87, 1);
  --ease-standard-out: cubic-bezier(0.33, 1, 0.68, 1);
  --ease-strong-out: cubic-bezier(0.25, 1, 0.5, 1);
  --ease-heavy-out: cubic-bezier(0, 0.55, 0.45, 1);
  --ease-expressive-out: cubic-bezier(0.34, 1.56, 0.64, 1);
}
```

Use these as a compact palette, not a requirement to define a full easing scale in every project.

### Use sparingly

- `ease-in`
  Avoid for ordinary UI entry or response.
- `back`
  Use only when a little overshoot adds clear personality or emphasis.
- `anticipate`
  Use only where the reverse motion helps communicate intent instead of adding friction.
- `jump`
  Treat as a niche, style-driven effect. It is usually wrong for general product UI.

### 4. How fast should it be?

| Element                  | Duration  |
| ------------------------ | --------- |
| press feedback           | 100-160ms |
| tooltips, small popovers | 125-200ms |
| dropdowns, selects       | 150-250ms |
| modals, drawers          | 200-500ms |

Ordinary UI motion should usually stay under 300ms.

## Perceived performance

The perception of speed matters as much as actual speed.

- Fast, responsive motion makes the product feel faster.
- Once one tooltip is open, nearby tooltips should appear instantly with no delay or animation.
- Faster open/close timings often make the whole app feel more capable.

### UX laws for motion

- **Doherty Threshold**: interaction should keep users and system in rhythm. Provide visible feedback within 400ms, and make repeated controls feel faster than occasional transitions.
- **Goal-Gradient Effect**: users become more motivated as they get closer to a goal. Progress motion should clarify advancement without slowing the task.
- **Peak-End Rule**: users remember the most intense moment and the end of an experience. Reserve expressive motion for meaningful peaks and clean completion states.

## Tooltips

Use an initial delay to avoid accidental activation, but once a tooltip is already open, adjacent tooltips should appear instantly.

```css
.tooltip[data-instant] {
  transition-duration: 0ms;
}
```

This preserves the purpose of the first delay while making dense toolbars feel faster.

## Buttons and press feedback

Pressable elements should feel responsive.

Use a subtle scale on press:

```css
.button {
  transition: transform 160ms ease-out;
}

.button:active {
  transform: scale(0.96);
}
```

Keep it subtle. `0.95` to `0.98` is the useful range. If the component supports a static mode, allow disabling the effect.

## Never animate from `scale(0)`

Elements should not appear from nothing.

```css
.entering {
  transform: scale(0.95);
  opacity: 0;
}
```

Use a visible starting scale plus opacity instead.

## Origin-aware motion

Popovers should scale from their trigger, not from the center. Modals are the exception and should stay centered.

```css
.popover {
  transform-origin: var(--radix-popover-content-transform-origin);
}
```

Base UI equivalent:

```css
.popover {
  transform-origin: var(--transform-origin);
}
```

## Interruptible animations

Interactive state changes should prefer CSS transitions because they retarget smoothly when the user changes intent mid-motion.

```css
.drawer {
  transform: translateX(-100%);
  transition: transform 200ms ease-out;
}

.drawer.open {
  transform: translateX(0);
}
```

Reserve keyframes for staged, one-shot sequences. For dynamic UI, transitions feel more natural.

## Enter animations

Split content into semantic chunks instead of animating one large block. Stagger children with short delays.

Useful ingredients:

- `opacity`
- small `translateY`
- subtle `blur`

Keep stagger delays short, usually 30-100ms between items.

If using Motion or Framer Motion, use `initial={false}` on `AnimatePresence` when you want to skip page-load animation for default-state UI.

Modern CSS entry animation can use `@starting-style` where supported.

```css
.toast {
  opacity: 1;
  transform: translateY(0);
  transition:
    opacity 400ms ease,
    transform 400ms ease;

  @starting-style {
    opacity: 0;
    transform: translateY(100%);
  }
}
```

## Exit animations

Exit motion should be softer and faster than enter motion.

Prefer a small fixed offset such as `translateY(-12px)` instead of moving the full element height unless spatial context truly matters.

Asymmetric timing is often right: slower while the user is deciding, faster when the system responds. Hold-to-confirm and hold-to-delete patterns are the clearest example.

## Content swaps

When swapping one visible state for another, do not rely on conditional rendering that instantly removes one node and mounts the next. Keep both states in the DOM long enough to transition between them.

This applies to text, icons, components, and even images. The goal is to avoid the feeling of a sudden replacement.

For text swaps such as `Copy` to `Copied!`, use `opacity` and `blur`. Delay the entering state slightly so the exiting state has time to fade and the two labels do not visually collide.

For icon swaps, use `opacity`, `blur`, and `scale`.

For larger component or image swaps, the same principle still applies: overlap the outgoing and incoming states briefly and fade between them instead of snapping from one to the next.

Rules:

- text: `opacity + blur`
- icon: `opacity + blur + scale`
- component or image swaps: overlap briefly and cross-fade instead of snapping
- add a small delay to the entering state
- prefer cross-fading over abrupt mount and unmount
- avoid visible layout shift during the swap

This usually produces a cleaner result than plain conditional render because the user perceives a transition, not a replacement.

When text changes inside a button, keep the button width stable. If the label lengths differ, either reserve enough width for both states or animate the width change so it does not feel like layout shift.

## Contextual icon animations

When icons swap on hover or state change, animate `opacity`, `scale`, and `blur` instead of abruptly replacing them.

Recommended values:

- scale: `0.25` to `1`
- opacity: `0` to `1`
- blur: `4px` to `0`

If Motion is available:

```tsx
transition={{ type: "spring", duration: 0.3, bounce: 0 }}
```

Without Motion, keep both icons in the DOM and cross-fade with CSS so both enter and exit are visible.

## Blur as a transition helper

If a crossfade feels visually wrong, a small blur can bridge the overlap and make the transformation read as one object changing instead of two objects swapping.

Keep blur subtle. Heavy blur is expensive, especially in Safari.

## Springs

Springs are useful when motion should feel alive, interruptible, or momentum-based:

- drag interactions
- decorative mouse-tracking effects
- gesture-driven UI
- playful components that benefit from natural settling

Recommended configurations:

```js
{ type: "spring", duration: 0.5, bounce: 0.2 }
```

or

```js
{ type: "spring", mass: 1, stiffness: 100, damping: 10 }
```

Keep bounce restrained. Most UI should use little or no bounce.

## Transforms and `clip-path`

Use percentages in `translate()` when you want movement relative to the element's own size.

```css
.drawer-hidden {
  transform: translateY(100%);
}
```

`scale()` also scales children, which is usually what you want for press feedback.

`clip-path` is useful for reveal interactions, hold-to-confirm patterns, comparison sliders, and image reveals.

```css
.overlay {
  clip-path: inset(0 100% 0 0);
  transition: clip-path 200ms ease-out;
}
```

WAAPI is a good option when you need programmatic control with CSS-like performance.

```js
element.animate(
  [{ clipPath: "inset(0 0 100% 0)" }, { clipPath: "inset(0 0 0 0)" }],
  {
    duration: 1000,
    fill: "forwards",
    easing: "cubic-bezier(0.77, 0, 0.175, 1)",
  },
);
```

3D transforms can add real depth when the effect truly benefits from it:

```css
.wrapper {
  transform-style: preserve-3d;
}
```

Use them sparingly. Most product UI does not need them, but they can work for deliberate depth effects, orbiting visuals, and similar expressive motion.

## Gesture guidance

For drag and dismissal patterns:

- consider velocity, not just distance
- apply damping near boundaries
- use pointer capture during drag
- ignore extra touch points after drag begins
- prefer friction over invisible hard stops

Quick flicks should dismiss when intent is clear even if distance is small.

## Accessibility

Respect reduced motion:

```css
@media (prefers-reduced-motion: reduce) {
  .element {
    animation: fade 0.2s ease;
  }
}
```

Reduced motion means fewer and gentler animations, not necessarily zero animation. Keep opacity or color transitions that improve comprehension and remove unnecessary movement.

Gate hover-only effects on devices that genuinely support hover:

```css
@media (hover: hover) and (pointer: fine) {
  .element:hover {
    transform: scale(1.05);
  }
}
```

## Cohesion

Animation values should match the personality of the component and product. Crisp professional UI wants different motion than a playful consumer component.

Review motion with fresh eyes, in slow motion, and on real devices when gestures matter.

## Reusable component lessons

When building a shared component, remember:

- Good defaults are usually more valuable than many configuration knobs.
- Motion, visuals, naming, and documentation should feel like one coherent product.
- Edge cases such as hidden tabs pausing timers, stacked hover gaps preserving hover state, interrupted drags, and repeated triggers should be handled invisibly.
