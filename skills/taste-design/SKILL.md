---
name: taste-design
description: Semantic Design System Skill. Generates AI Agent-friendly DESIGN.md files for Tailwind projects that enforce premium, anti-generic UI standards — strict typography, calibrated color, asymmetric layouts, perpetual micro-motion, and hardware-accelerated performance.
allowed-tools:
  - "Read"
  - "Write"
  - "web_fetch"
---

# Design Taste — Semantic Design System Skill

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

所有輸出內容必須使用**繁體中文**，包含：

- 所有描述性文字（atmosphere、功能說明、anti-patterns 說明）
- DESIGN.md 的 section 標題與說明段落
- 與使用者的所有溝通

以下內容保持英文原文，不翻譯：

- Tailwind class 名稱（`bg-zinc-950`、`text-5xl` 等）
- Hex 色碼（`#18181B`）
- 字體名稱（`Geist`、`Satoshi` 等）
- CSS 屬性與數值
- Motion 參數

## Analysis & Synthesis Instructions

### 1. Define the Atmosphere

Evaluate the target project's intent. Use evocative adjectives to describe the mood, density, and motion intensity. Keep it brief and directional — this is for AI Agent consumption, not a design brief narrative.

- **Mood** — the emotional register (e.g. clinical, warm, playful, editorial)
- **Density** — information compactness (e.g. airy / balanced / dense)
- **Motion intensity** — how much animation is present (e.g. static / fluid / cinematic)

### 2. Map the Color Palette

For each color provide: **Descriptive Name** + **Tailwind Token** + **Hex Code** + **Functional Role**.

**Color direction workflow（依序執行）：**

1. 讀取 `BRAND.md`，掌握品牌調性與情境
2. 確認使用者是否已有明確色彩偏好（偏好色、禁用色、既有品牌主色）
3. 若使用者有明確偏好，優先以該偏好為準
4. 若使用者沒有偏好，從 `BRAND.md` 與專案 context 推導品牌色方向
5. 若專案已有 token schema（如 shadcn/ui CSS variables），沿用 token 結構與命名，但依品牌方向重新校準 token values — 不因 token 已存在就沿用預設配色

**Mandatory constraints:**

- Maximum 1 accent color. Saturation below 80%
- The "AI Purple/Blue Neon" aesthetic is strictly BANNED — no purple button glows, no neon gradients
- Use absolute neutral bases (Zinc/Slate) with high-contrast singular accents
- Stick to one palette for the entire output — no warm/cool gray fluctuation
- Never use pure black (`#000000`) — use Off-Black, `zinc-950`, or Charcoal

### 3. Establish Typography Rules

Use Tailwind classes for size, weight, and spacing. Font selection uses font family names mapped to Tailwind's `font-sans`, `font-serif`, and `font-mono` utilities:

- **Display/Headlines:** `font-sans text-5xl font-semibold tracking-tight` — hierarchy through weight and color, not just massive size
- **Body:** `font-sans text-base leading-relaxed max-w-[65ch]` — relaxed leading, max 65 characters per line
- **Mono:** `font-mono` — for code, metadata, timestamps, high-density numbers
- **Font Selection:** `Inter` is BANNED for premium/creative contexts. Force unique character: `Geist`, `Outfit`, `Cabinet Grotesk`, or `Satoshi` — configured as `font-sans` in Tailwind theme
- **Serif Ban:** Generic serif fonts (`Times New Roman`, `Georgia`, `Garamond`) are BANNED. If serif is needed for editorial/creative contexts, use only distinctive modern serifs: `Fraunces`, `Editorial New`, or `Instrument Serif` — configured as `font-serif`. Serif is always BANNED in dashboards or software UIs
- **Dashboard Constraint:** `font-sans` + `font-mono` pairings exclusively (`Geist` + `Geist Mono` or `Satoshi` + `JetBrains Mono`)
- **High-Density Override:** When density exceeds 7, all numbers must use `font-mono`

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
