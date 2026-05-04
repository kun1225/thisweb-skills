---
name: design-md
description: Semantic Design System Skill. Generates AI Agent-friendly DESIGN.md files for Tailwind projects that enforce premium, anti-generic UI standards — strict typography, calibrated color, asymmetric layouts, perpetual micro-motion, and hardware-accelerated performance.
allowed-tools:
  - "Read"
  - "Write"
  - "web_fetch"
---

Generate a `DESIGN.md` for a Tailwind project. The file is consumed by AI Agents to produce new screens — write rules that are precise, scannable, and immediately actionable. Read `references/DESIGN.md` for the output template; fill every section with project-specific values.

## The Goal

Generate a `DESIGN.md` file that encodes:

1. **Visual atmosphere** — the mood, density, and motion intensity
2. **Color calibration** — neutrals, accents, and banned patterns with Tailwind tokens and hex codes
3. **Typographic architecture** — font stacks, Tailwind scale classes, and anti-patterns
4. **Component behaviors** — buttons and cards with Tailwind class descriptions
5. **Layout principles** — grid systems, spacing philosophy, and baseline responsive constraints
6. **Motion philosophy** — Motion animation specs, spring physics, perpetual micro-interactions
7. **Anti-patterns** — explicit list of banned AI design clichés

## Step 0 — Establish Brand Context

1. **BRAND.md exists** → Read it. Use as source of truth.
2. **No BRAND.md, but context exists** → Synthesize a minimal `BRAND.md` from README, components, or user description. Write it to the project root, then continue.
3. **No BRAND.md, no context** → Fetch `https://raw.githubusercontent.com/kun1225/thisweb-skills/main/skills/web-brand-md/SKILL.md` and run its interview flow to generate `BRAND.md` first.

## Language Rules

- **DESIGN.md content**: Traditional Chinese for all descriptive text, section titles, and body copy
- **Stay English**: Tailwind classes, hex codes, font names, CSS values, Motion parameters
- **User communication**: Traditional Chinese

## 1. Atmosphere

Three short descriptors:

- **Mood** — emotional register (e.g. clinical, warm, editorial)
- **Density** — information compactness (e.g. airy / balanced / dense)
- **Motion intensity** — animation presence (e.g. static / fluid / cinematic)

## 2. Color Palette

**Output format per color:**

```
- [semantic name]（#HEX）— [descriptive color name]：[functional role]
```

**Example:**

```
- primary（#31594A）— 森林綠：唯一強調色，用於 CTA、active 狀態、focus ring
- background（#F9FAFB）— 畫布白：主要背景底色
- foreground（#18181B）— 炭墨黑：主要文字
```

**Required tokens:** `primary`, `background`, `surface`, `foreground`, `muted`, `border`. Add `secondary` / `tertiary` only when multiple accent levels are genuinely needed — max 3 total.

**Decision workflow:**

1. Read `BRAND.md` for tone and color direction
2. Honor explicit user preferences (preferred colors, banned colors, existing brand)
3. If no preferences, derive from brand context
4. If an existing token schema exists (e.g. shadcn/ui CSS variables), keep the structure but recalibrate values — never carry over defaults just because tokens exist

**Constraints:**

- Max 1 accent. Saturation below 80%
- No "AI Purple/Blue Neon" — no purple glows, no neon gradients
- Neutral base: Zinc or Slate only — no warm/cool gray mixing
- No pure black (`#000000`) — use Off-Black or `zinc-950`

## 3. Typography

**Step 0 — Confirm project language:**

Check the project's primary content language before selecting fonts. The font stack differs significantly between Latin and CJK contexts.

- **Latin only** (English, European languages) → use Latin typefaces from the Policy list below
- **CJK primary** (Traditional Chinese, Simplified Chinese, Japanese, Korean) → pair a Latin display font with a CJK system stack: `"Noto Sans TC", "PingFang TC", "Microsoft JhengHei", sans-serif`; avoid decorative Latin fonts for body text — they render poorly with CJK glyphs
- **Mixed** (Latin UI + CJK content) → assign Latin fonts to display/heading tokens (`font-hero`, `font-title`), CJK stack to body tokens (`font-body-lg`, `font-body-sm`)

If the project language is ambiguous, ask before assigning fonts.

**Type scale:**

| Level        | Font Token      | Tailwind Classes                         | Usage                                                |
| ------------ | --------------- | ---------------------------------------- | ---------------------------------------------------- |
| **Hero**     | `font-hero`     | `text-6xl font-bold tracking-tight`      | Page hero statement, banner. Max once per page.      |
| **Title**    | `font-title`    | `text-4xl font-semibold tracking-tight`  | Section headings, H1                                 |
| **Subtitle** | `font-subtitle` | `text-2xl font-medium tracking-tight`    | Card headings, H2/H3, module labels                  |
| **Body-lg**  | `font-body-lg`  | `text-lg leading-relaxed max-w-[65ch]`   | Long-form articles, landing page lead paragraphs     |
| **Body-sm**  | `font-body-sm`  | `text-base leading-relaxed max-w-[65ch]` | General body, sidebar descriptions, form helper text |
| **Caption**  | `font-caption`  | `text-sm leading-normal text-muted`      | Image captions, dates, metadata                      |
| **Label**    | `font-label`    | `text-sm font-medium tracking-wide`      | Button text, tags, badges, form labels               |
| **Mono**     | `font-mono`     | `text-sm`                                | Code, SKUs, timestamps, high-density numbers         |

**Policy:**

- Token names must map 1:1 to semantic levels — no shared family tokens like `font-sans` or `font-display`
- Only add `-lg` / `-sm` variants when the same level serves two clearly distinct contexts
- `Inter` is BANNED — use `Geist`, `Outfit`, `Cabinet Grotesk`, or `Satoshi`
- Generic serifs (`Times New Roman`, `Georgia`, `Garamond`) are BANNED — if serif is needed, use `Fraunces`, `Editorial New`, or `Instrument Serif`
- Dashboard / software UI: serif-backed title tokens are BANNED
- When density > 7, all numbers use `font-mono`

## 4. Component Stylings

**Rule:** Every color-bearing Tailwind class (`text-*`, `bg-*`, `border-*`, `ring-*`, `shadow-*`, `hover:*`, `from-*`/`to-*`, etc.) must use only the semantic tokens defined in Section 2.

**Token → class reference:**

| Intent                  | Correct class         | Banned examples                          |
| ----------------------- | --------------------- | ---------------------------------------- |
| Primary text            | `text-foreground`     | `text-zinc-900`, `text-[#1a1a1a]`        |
| Secondary / meta text   | `text-muted`          | `text-zinc-500`, `text-[#888]`           |
| Accent / CTA text       | `text-primary`        | `text-green-600`, `text-[#31594A]`       |
| Page background         | `bg-background`       | `bg-zinc-50`, `bg-[#f9fafb]`             |
| Card / surface fill     | `bg-surface`          | `bg-white`, `bg-zinc-100`                |
| Accent fill             | `bg-primary`          | `bg-emerald-600`, `bg-[#31594A]`         |
| Reversed text on accent | `text-background`     | `text-white`, `text-[#fff]`              |
| Dividers / borders      | `border-border`       | `border-zinc-200`, `border-[#ddd]`       |
| Hover state fill        | `hover:bg-primary/10` | `hover:bg-zinc-100`, `hover:bg-[#eee]`   |
| Focus ring              | `ring-primary`        | `ring-zinc-400`, `ring-[#999]`           |
| Shadow tint             | `shadow-border/50`    | `shadow-zinc-200/50`, `shadow-[#ccc]/30` |

**Components:**

- **button:** `bg-foreground text-background px-6 py-2.5 rounded-xl font-medium transition-all duration-200 hover:bg-foreground/90 active:-translate-y-px focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-primary` — no outer glows, tactile push on active
- **Card:** `rounded-2xl border border-border bg-surface p-6 shadow-sm shadow-border/50 hover:shadow-md hover:shadow-border/30 transition-shadow duration-200` — use shadows only when elevation communicates hierarchy; high-density layouts use `border-t border-border` dividers instead

## 5. Layout Principles

- Grid-first responsive architecture. Contain with `max-w-8xl mx-auto`
- Asymmetric splits preferred — use Split Screen, Left-Aligned, or Asymmetric Whitespace over centered layouts
- All multi-column layouts collapse to single column below `md:`
- All interactive elements: `min-h-11`

## 6. Motion

CSS-first. Use Motion library only for: spring physics, staggered orchestration, perpetual loops.

**Easing selection (3 steps):**

1. **Pick a family** — `SINE` (softest) → `QUAD`/`CUBIC` (everyday UI) → `QUART`/`QUINT` (emphatic) → `EXPO` (dramatic) → `BACK`/`ANTICIPATE` (springy). See `references/EASING.md` for full table.
2. **Pick direction** — `Out` (entering, most common) · `InOut` (cross-screen) · `In` (exiting, rarely)
3. **Apply value:**

```
cubicOut:    cubic-bezier(0.33, 1, 0.68, 1)     ← default for hover & enter
cubicInOut:  cubic-bezier(0.66, 0, 0.34, 1)     ← cross-screen moves
quartOut:    cubic-bezier(0.25, 1, 0.5, 1)      ← emphatic entrances
backOut:     cubic-bezier(0.34, 1.56, 0.64, 1)  ← springy popovers / toasts
```

**Common patterns:**

- Hover: `transition-[property] duration-200 ease-[cubicOut]`
- Enter / leave: `transition-[property] duration-300 ease-[cubicOut]`
- Cross-screen: `transition-[property] duration-500 ease-[cubicInOut]`
- Spring (Motion): `transition={{ type: "spring", stiffness: 100, damping: 20, mass: 1 }}`
- Snappy spring: `transition={{ type: "spring", stiffness: 300, damping: 25, mass: 0.5 }}`

Animate only `transform` and `opacity`. Never animate layout properties (`top`, `left`, `width`, `height`).

## 7. Anti-Patterns

- No emojis
- No `Inter`, no generic serifs (`Times New Roman`, `Georgia`, `Garamond`)
- No pure black (`#000000`)
- No neon / outer glow shadows
- No oversaturated accents
- No excessive gradient text on large headers
- No custom mouse cursors
- No 3-column equal card layouts — use 2-column Zig-Zag, asymmetric grid, or horizontal scroll
- No overlapping elements
- No generic placeholder names ("John Doe", "Acme", "Nexus")
- No fabricated data — use `[metric]` labels, not invented numbers
- No `LABEL // YEAR` formatting
- No AI copywriting clichés ("Elevate", "Seamless", "Unleash", "Next-Gen")
- No filler UI: "Scroll to explore", scroll arrows, bouncing chevrons
- No broken Unsplash links — use `picsum.photos` or SVG avatars

## Output Format

Read `references/DESIGN.md` and fill each section with project-specific values. Do not add, remove, or reorder sections.
