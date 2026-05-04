# Easing Reference

Full easing dictionary for motion design. The main SKILL.md covers the 4 most common values — use this file when a project needs a less common easing family.

## Easing Family Guide

| Family         | Feel                                                        | Best for                                                                     |
| -------------- | ----------------------------------------------------------- | ---------------------------------------------------------------------------- |
| **SINE**       | Softest and most natural — smooth at both ends              | Hover, fade, low-distraction transitions, lightweight brands                 |
| **QUAD**       | Gentle acceleration/deceleration — more dynamic than linear | Everyday UI, buttons, cards, basic interface animations                      |
| **CUBIC**      | Moderate acceleration — confident and stable                | Standard UI transitions, modals, drawers, panel slide-in/out                 |
| **QUART**      | Noticeable speed contrast — slow start, fast finish         | Tension-driven brand animations, hero element entrances                      |
| **QUINT**      | Strong acceleration/deceleration — powerful and rhythmic    | Dramatic transitions, large element movement, rhythm-heavy interactions      |
| **EXPO**       | Extreme speed contrast — nearly still then sudden burst     | Full-screen switches, hero animations, bold entrances (use sparingly)        |
| **CIRC**       | Weighted, inertia-like — follows a circular arc             | Tactile pop-ups, large cards and panels, elements that feel physically heavy |
| **JUMP**       | Discrete steps — close to `steps()`                         | Pixel art, counters, toggle states, mechanical or game UI                    |
| **BACK**       | Slightly overshoots the target — springy and lively         | Toasts, popovers, card entrances, success states, energetic brand UI         |
| **ANTICIPATE** | Pulls back before moving forward — wind-up effect           | Character-like animations, drag-release, key element reveals, playful UI     |

## Full cubic-bezier Values

```
sineOut:         cubic-bezier(0.61, 1, 0.87, 1)
sineInOut:       cubic-bezier(0.36, 0, 0.64, 1)
quadOut:         cubic-bezier(0.5, 1, 0.89, 1)
quadInOut:       cubic-bezier(0.44, 0, 0.56, 1)
cubicOut:        cubic-bezier(0.33, 1, 0.68, 1)
cubicInOut:      cubic-bezier(0.66, 0, 0.34, 1)
quartOut:        cubic-bezier(0.25, 1, 0.5, 1)
quartInOut:      cubic-bezier(0.78, 0, 0.22, 1)
quintOut:        cubic-bezier(0.22, 1, 0.36, 1)
quintInOut:      cubic-bezier(0.86, 0, 0.14, 1)
expoOut:         cubic-bezier(0.16, 1, 0.3, 1)
expoInOut:       cubic-bezier(0.9, 0, 0.1, 1)
circOut:         cubic-bezier(0, 0.55, 0.45, 1)
circInOut:       cubic-bezier(0.85, 0.09, 0.15, 0.91)
jumpInOut:       cubic-bezier(1, 0, 0, 1)
backOut:         cubic-bezier(0.34, 1.56, 0.64, 1)
backInOut:       cubic-bezier(0.68, -0.6, 0.32, 1.6)
anticipateInOut: cubic-bezier(0.8, -0.4, 0.5, 1)
```
