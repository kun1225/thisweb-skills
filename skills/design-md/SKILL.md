---
name: design-md
description: Semantic Design System Skill. Generates AI Agent-friendly DESIGN.md files for Tailwind projects that enforce premium, anti-generic UI standards — strict typography, calibrated color, asymmetric layouts, perpetual micro-motion, and hardware-accelerated performance.
allowed-tools:
  - "Read"
  - "Write"
  - "web_fetch"
---

## Overview

This skill generates `DESIGN.md` files optimized for AI Agent consumption in Tailwind-based projects. It translates battle-tested anti-slop frontend engineering directives into a semantic design language — descriptive, natural-language rules paired with precise Tailwind classes and values that AI Agents can interpret to produce premium, non-generic interfaces.

The generated `DESIGN.md` serves as the **single source of truth** for prompting AI Agents to generate new screens that align with a curated, high-agency design language.

## Step 0 — Read or Generate BRAND.md

Before generating the design system, establish brand context:

1. **BRAND.md found** — Read it. Use it as the source of truth for color direction, layout personality, and tone.
2. **BRAND.md not found, but sufficient context exists** — Synthesize a minimal one-shot `BRAND.md` from the available project context (README, existing components, user description). Write it to the project root before continuing.
3. **BRAND.md not found and context is insufficient** — Fetch `https://raw.githubusercontent.com/kun1225/thisweb-skills/main/skills/web-brand-md/SKILL.md` and follow its interview flow to generate `BRAND.md` first, then continue.

## The Goal

Generate a `DESIGN.md` file that encodes:

1. **Visual atmosphere** — the mood, density, and motion intensity
2. **Color calibration** — neutrals, accents, and banned patterns with Tailwind tokens and hex codes
3. **Typographic architecture** — font stacks, Tailwind scale classes, and anti-patterns
4. **Component behaviors** — buttons and cards with Tailwind class descriptions
5. **Layout principles** — grid systems, spacing philosophy, and baseline responsive constraints
6. **Motion philosophy** — Motion animation specs, spring physics, perpetual micro-interactions
7. **Anti-patterns** — explicit list of banned AI design clichés

## Language Rules

All output content must be written in **Traditional Chinese**, including:

- All descriptive text (atmosphere, functional descriptions, anti-pattern explanations)
- Section titles and body paragraphs in DESIGN.md
- All communication with the user

The following must remain in English as-is:

- Tailwind class names (`bg-zinc-950`, `text-5xl`, etc.)
- Hex color codes (`#18181B`)
- Font names (`Geist`, `Satoshi`, etc.)
- CSS properties and values
- Motion parameters

## Analysis & Synthesis Instructions

### 1. Define the Atmosphere

Evaluate the target project's intent. Use evocative adjectives to describe the mood, density, and motion intensity. Keep it brief and directional — this is for AI Agent consumption, not a design brief narrative.

- **Mood** — the emotional register (e.g. clinical, warm, playful, editorial)
- **Density** — information compactness (e.g. airy / balanced / dense)
- **Motion intensity** — how much animation is present (e.g. static / fluid / cinematic)

### 2. Map the Color Palette

For each color provide: **Semantic Name** + **Tailwind Token** + **Hex Code** + **Functional Role**.

**Color naming convention — output format for each color:**

```
- [semantic name]（#HEX）— [descriptive color name]：[functional role]
```

Example:

```
- primary（#31594A）— 森林綠：唯一強調色，用於 CTA、active 狀態、focus ring
- background（#F9FAFB）— 畫布白：主要背景底色
- foreground（#18181B）— 炭墨黑：主要文字
```

Fixed semantic name roles: `primary`, `background`, `surface`, `foreground`, `muted`, `border`. Add `secondary` and `tertiary` only when multiple accent levels are needed — maximum 3 total, each with saturation below 80%. Do not use Tailwind token names — hex codes only.

**Color direction workflow (execute in order):**

1. Read `BRAND.md` to understand brand tone and context
2. Check whether the user has explicit color preferences (preferred colors, banned colors, existing brand colors)
3. If the user has explicit preferences, prioritize them
4. If no preferences, derive the brand color direction from `BRAND.md` and project context
5. If the project already has a token schema (e.g. shadcn/ui CSS variables), keep the token structure and naming, but recalibrate token values to match the brand direction — do not carry over default color values just because tokens exist

**Mandatory constraints:**

- Maximum 1 accent color. Saturation below 80%
- The "AI Purple/Blue Neon" aesthetic is strictly BANNED — no purple button glows, no neon gradients
- Use absolute neutral bases (Zinc/Slate) with high-contrast singular accents
- Stick to one palette for the entire output — no warm/cool gray fluctuation
- Never use pure black (`#000000`) — use Off-Black, `zinc-950`, or Charcoal

### 3. Establish Typography Rules

Define a type scale from largest to smallest. Use semantic names — not numbers. Only add `-lg` / `-sm` variants when the same semantic level genuinely needs two distinct sizes with different use cases.

**Type scale (large → small):**

| Level        | Font           | Tailwind Classes                         | Usage                                                |
| ------------ | -------------- | ---------------------------------------- | ---------------------------------------------------- |
| **Hero**     | `font-display` | `text-6xl font-bold tracking-tight`      | Page hero statement, banner. Max once per page.      |
| **Title**    | `font-display` | `text-4xl font-semibold tracking-tight`  | Section headings, H1                                 |
| **Subtitle** | `font-sans`    | `text-2xl font-medium tracking-tight`    | Card headings, H2/H3, module labels                  |
| **Body-lg**  | `font-sans`    | `text-lg leading-relaxed max-w-[65ch]`   | Long-form articles, landing page lead paragraphs     |
| **Body-sm**  | `font-sans`    | `text-base leading-relaxed max-w-[65ch]` | General body, sidebar descriptions, form helper text |
| **Caption**  | `font-sans`    | `text-sm leading-normal text-muted`      | Image captions, dates, metadata                      |
| **Label**    | `font-sans`    | `text-sm font-medium tracking-wide`      | Button text, tags, badges, form labels               |
| **Mono**     | `font-mono`    | `text-sm`                                | Code, SKUs, timestamps, high-density numbers         |

**Rules:**

- Start with these 7 levels. Only add variants (e.g. `Body-lg` / `Body-sm`) when two sizes share the same semantic role but serve clearly different contexts.
- `Inter` is BANNED for premium/creative contexts. Force unique character: `Geist`, `Outfit`, `Cabinet Grotesk`, or `Satoshi` — configured as `font-sans`
- Generic serif fonts (`Times New Roman`, `Georgia`, `Garamond`) are BANNED. If serif is needed, use only: `Fraunces`, `Editorial New`, or `Instrument Serif` — configured as `font-display`
- Dashboard constraint: `font-sans` + `font-mono` only — `font-display` is BANNED in dashboards or software UIs
- When density exceeds 7, all numbers must use `font-mono`

### 4. Describe Component Stylings

For each component type, describe shape, color, shadow depth, and interaction behavior using Tailwind classes:

- **Buttons:** Tactile push feedback on active state (`active:-translate-y-px`). No neon outer glows. No custom mouse cursors. Example: `bg-zinc-900 text-white px-6 py-2.5 rounded-xl font-medium transition-transform active:-translate-y-px`
- **Cards:** Use ONLY when elevation communicates hierarchy. Tint shadows to background hue (`shadow-zinc-200/50`). For high-density layouts, replace cards with `border-t` dividers or negative space. Example: `rounded-2xl border border-zinc-100 bg-white p-6 shadow-sm shadow-zinc-200/50`

### 5. Define Layout Principles

- No overlapping elements — every element occupies its own clear spatial zone
- Centered layouts BANNED for asymmetric or creative projects — force Split Screen, Left-Aligned, or Asymmetric Whitespace
- The generic "3 equal cards horizontally" feature row is BANNED — use 2-column Zig-Zag, asymmetric grid, or horizontal scroll
- Contain layouts using max-width constraints (`max-w-7xl mx-auto`)
- **Baseline responsive constraints (non-negotiable):**
  - All multi-column layouts collapse to single column below `md:` breakpoint
  - All interactive elements minimum `44px` tap target (`min-h-[44px]`)

### 6. Encode Motion Philosophy

Prefer CSS transitions for all interactive elements. Only use the Motion library when CSS cannot achieve the required effect (e.g. spring physics, staggered orchestration, perpetual loops).

**CSS-first easing patterns:**

- **Hover:** `transition-[property] duration-200 ease-[cubic-bezier(0.4,0,0.2,1)]` — snappy, responsive
- **Enter & Leave:** `ease-out` — elements decelerate into place
- **Element moving across screen:** `ease-in-out` — smooth acceleration and deceleration

**When Motion is required, provide copy-paste spring parameters:**

- **Spring default:** `transition={{ type: "spring", stiffness: 100, damping: 20, mass: 1 }}` — premium, weighty feel
- **Snappy spring (hover/micro):** `transition={{ type: "spring", stiffness: 300, damping: 25, mass: 0.5 }}`
- **Perpetual Micro-Interactions:** `animate` with `repeat: Infinity` — Pulse, Typewriter, Float, Shimmer
- **Staggered Orchestration:** `staggerChildren` with `delayChildren` for waterfall list reveals

**Performance rules (always):** Animate exclusively via `transform` and `opacity`. Never animate `top`, `left`, `width`, `height`.

### 7. List Anti-Patterns (AI Tells)

Encode these as explicit "NEVER DO" rules in the DESIGN.md:

- No emojis anywhere
- No `Inter` font
- No generic serif fonts (`Times New Roman`, `Georgia`, `Garamond`) — distinctive modern serifs only if needed
- No pure black (`#000000`)
- No neon/outer glow shadows
- No oversaturated accents
- No excessive gradient text on large headers
- No custom mouse cursors
- No overlapping elements — clean spatial separation always
- No 3-column equal card layouts
- No generic names ("John Doe", "Acme", "Nexus")
- No fake round numbers (`99.99%`, `50%`)
- No fabricated data or statistics — never generate metrics, performance numbers, uptime percentages, response times, or any data that the user did not explicitly provide. Use clear placeholder labels like `[metric]` instead
- No fake system/metric sections — "SYSTEM PERFORMANCE METRICS", "KEY STATISTICS" dashboard cards filled with invented data are BANNED
- No `LABEL // YEAR` formatting — lazy AI convention, not real design typography
- No AI copywriting clichés ("Elevate", "Seamless", "Unleash", "Next-Gen")
- No filler UI text: "Scroll to explore", "Swipe down", scroll arrows, bouncing chevrons
- No broken Unsplash links — use `picsum.photos` or SVG avatars

## Output Format (DESIGN.md Structure)

Read `references/DESIGN.md` and fill in each section. Do not add, remove, or reorder any sections.

## Best Practices

- **Use Tailwind classes:** Write `rounded-2xl` and `text-5xl tracking-tight`, not vague descriptions like "generously rounded" or "track-tight scale"
- **Be Functional:** Explain what each element is used for
- **Be Consistent:** Same Tailwind class terminology throughout the document
- **Be Precise:** Include exact Tailwind tokens, hex codes, and rem values
- **Be Opinionated:** This is not a neutral template — it enforces a specific, premium aesthetic
- **Derive from brand:** Color and layout direction should reflect the `BRAND.md` context

## Common Pitfalls to Avoid

- Using vague descriptions instead of Tailwind classes ("generously rounded" → use `rounded-2xl`)
- Omitting Tailwind tokens or using only descriptive color names
- Forgetting functional roles of design elements
- Defaulting to generic "safe" designs instead of enforcing the curated aesthetic
- Ignoring the anti-pattern list — these are what make the output premium
- Fabricating brand colors without reading `BRAND.md` first
