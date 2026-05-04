---
name: logo-generator
description: >
  Generate professional SVG logos and high-end showcase images. Use when the user wants to: (1) Create a logo or icon for their product/brand, (2) Generate logo design concepts based on product information, (3) Create professional logo showcase presentations with multiple background styles, (4) Export logos in various formats (SVG, PNG), or (5) Iterate on logo designs with different visual styles. Supports geometric patterns, dot matrix designs, line systems, mixed compositions, and Codex imagegen-based showcase images with 12 professional background styles.
---

# Logo Generator

Generate professional SVG logos and high-end showcase presentations for products and brands.

## Workflow

### Phase 1: Information Gathering

Collect essential information from the user:

1. **Product/Brand Name** (required)
2. **Industry/Category** (e.g., AI, fintech, design tools)
3. **Core Concept** (e.g., connection, flow, security, simplicity)
4. **Design Preferences**:
   - Style: minimal/complex, geometric/organic
   - Color preference: monochrome/specific colors
   - Mood: cold/warm, professional/friendly

Ask concise questions to gather this information. Don't overwhelm the user with too many questions at once.

### Phase 2: Pattern Matching & SVG Generation

Based on the gathered information:

1. **Generate at least 6 design variants** based on `references/design_patterns.md`
   - Match patterns to product characteristics
   - Use different pattern types and combinations for diversity
   - Include both single-pattern and mixed-pattern compositions
   - Vary complexity levels (simple geometric to layered compositions)
   - Each variant should feel distinctly different, not just parameter tweaks
   - Explain the design rationale for each variant

2. **Generate SVG code** for each variant
   - Use viewBox="0 0 100 100" for easy scaling
   - Keep code clean and well-structured
   - Use `currentColor` for flexible color control
   - Add subtle animations for web display (optional)

3. **Create interactive showcase webpage**
   - Display all 6+ logo variants in a grid layout
   - Use the template from `assets/showcase_template.html`
   - Include hover effects and smooth transitions
   - Add design rationale for each variant
   - Allow easy comparison between variants

### Phase 3: Iteration & Refinement

Allow user to provide feedback:

- Select favorite variants (narrow down from 6+ to 2-3)
- Adjust specific parameters (size, spacing, rotation)
- Combine elements from different variants
- Change colors or add gradients
- Modify animations or effects
- Generate additional variants exploring specific directions

Make targeted adjustments based on feedback. Don't regenerate everything unless requested.

### Phase 4: High-End Showcase Generation

Once the user selects a preferred logo direction:

1. **Export SVG to PNG**
   - Use `scripts/svg_to_png.py` to convert SVG to PNG
   - Default size: 1024x1024px
   - Ensure transparent background

2. **Select showcase styles**
   - Review `references/background_styles.md`
   - Recommend 4 styles based on product type and mood
   - Explain why each style fits

3. **Generate showcase images with Codex imagegen**
   - Use the exported PNG as the logo reference
   - Read `references/background_styles.md` and select the best 4 styles
   - Call the Codex `imagegen` skill/tool for each selected style
   - Keep the logo flat, sharp, centered, and high-contrast
   - Preserve the core logo geometry instead of redesigning the mark

4. **Create final presentation webpage**
   - Combine SVG variants and showcase images
   - Use professional layout with micro-typography
   - Include download links for all assets

### Phase 5: Delivery

Provide the user with:

- Interactive HTML showcase page
- SVG files (editable vector format)
- PNG exports (various sizes if requested)
- Showcase images (4 professional backgrounds)

## Key Design Principles

1. **Provide Variety**: Generate at least 6 distinct variants to give users real choices
2. **Start Simple**: Begin with basic patterns, add complexity only when needed
3. **Meaningful Design**: Connect visual elements to product concepts
4. **Scalability**: Ensure logos work at all sizes
5. **Professional Quality**: Match high-end brand identity standards
6. **Flexibility**: Provide multiple variants for different use cases

## Technical Notes

### SVG Best Practices

- Keep viewBox at `0 0 100 100` for consistency
- Use semantic grouping with `<g>` tags
- Leverage `<defs>` for reusable elements
- Use `<clipPath>` for masking effects
- Prefer geometric primitives over complex paths when possible

### PNG Export

The `svg_to_png.py` script requires:
- Python 3.8+
- Dependencies: `pip install -r requirements.txt`
- Reference SVG file

### Showcase Image Generation

Use Codex image generation for final showcase images. Build each prompt from:
- The exported logo PNG as visual reference
- One selected style from `references/background_styles.md`
- Product name, product description, and desired brand mood

Prompt requirements:
- Extract the core logo graphic from the reference image
- Render the logo as a pure flat vector-like shape
- Use white logo on dark backgrounds and black logo on light backgrounds
- Center the logo with generous breathing room
- Add only micro-typography, never large titles
- Keep the showcase presentation restrained, premium, and brand-system oriented

### Available Background Styles

From `references/background_styles.md`:

**12 Professional Styles Available**:

**Dark Styles** (6):
- void (绝对虚空) - Absolute minimalism, hardcore tech
- frosted (磨砂穹顶) - Modern breathing space, premium products
- fluid (流体深渊) - AI-native fluidity, dynamic systems
- spotlight (物理影棚) - Studio lighting, editorial quality
- analog_liquid (物理流体) - Metallic shimmer on solid color base, creative brands
- led_matrix (数字硬件) - Digital retro, cyberpunk aesthetics

**Light Styles** (6):
- editorial (纸本编辑) - Specialty paper, humanistic brands
- iridescent (幻彩透砂) - Optical materials, tech hardware
- morning (晨雾光域) - AI softness, approachable products
- clinical (无菌影棚) - Spatial order, algorithm-driven brands
- ui_container (容器化界面) - Digital product native, SaaS platforms
- swiss_flat (瑞士扁平) - Absolute flatness, timeless authority

Each style has specific visual characteristics and suitable use cases. Consult the reference document for details.

## Common Patterns

### Pattern: Concentric Circle Dots
```svg
<svg viewBox="0 0 100 100">
  <g>
    <!-- Inner ring: 6 dots -->
    <circle cx="50" cy="38" r="3" fill="currentColor"/>
    <!-- Add more dots in circular arrangement -->
  </g>
</svg>
```

### Pattern: Geometric Shape with Line Accent
```svg
<svg viewBox="0 0 100 100">
  <polygon points="50,30 70,60 30,60" fill="none" stroke="currentColor" stroke-width="2"/>
  <circle cx="50" cy="30" r="4" fill="currentColor"/>
</svg>
```

### Pattern: Node Network
```svg
<svg viewBox="0 0 100 100">
  <path d="M 30 70 Q 50 70, 50 50 T 70 30" stroke="currentColor" stroke-width="2" fill="none"/>
  <circle cx="30" cy="70" r="4" fill="currentColor"/>
  <circle cx="50" cy="50" r="5" fill="currentColor"/>
  <circle cx="70" cy="30" r="4" fill="currentColor"/>
</svg>
```

For more patterns and combinations, see `references/design_patterns.md`.

## Troubleshooting

**SVG not displaying correctly**: Check viewBox and ensure all paths are closed

**PNG export fails**: Verify cairosvg is installed (`pip install cairosvg`)

**Showcase generation fails**:
- Verify the reference PNG exists and is readable
- Simplify the imagegen prompt to one style and one logo reference
- Regenerate only the failed style instead of the full set
