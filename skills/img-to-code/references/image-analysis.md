# Image Analysis

Analyze images cleanly and systematically before writing code.

Do not do vague vibe-only analysis.
Do not jump too quickly from image to implementation.

Treat the image like a design specification.

## Clean analysis standard

For every image, inspect:

- what the section or screen is
- what the visual priority is
- what text is clearly readable
- what typography relationships are visible
- what spacing relationships are visible
- what buttons and controls are visible
- what card or block logic is visible
- what colors dominate
- what structural rhythm is visible
- what details are still unclear

If something important is unclear, say so explicitly before coding.

The analysis should feel:

- calm
- structured
- exact
- faithful
- design-aware
- implementation-aware

## Deep image analysis requirements

Before implementing anything, deeply inspect and extract:

- exact visible text where readable
- hero headline wording
- subheadline wording
- CTA wording
- section titles
- typography character
- type scale relationships
- font mood
- line count
- line wrapping behavior
- alignment logic
- section spacing
- internal spacing
- padding and gutters
- card dimensions and rhythm
- border radius logic
- stroke and divider usage
- button shapes
- button hierarchy
- button padding
- hover-implied styling if visually suggested
- color palette
- accent colors
- background treatment
- image treatment
- icon treatment
- shadows and depth logic
- grid logic
- layout structure
- section ordering
- section density
- visual rhythm
- repeated motifs that define the design language

Your goal is to understand why the design looks strong, not just what it contains.

## Text extraction

When text is readable in the image, extract it and use it.

Especially inspect:

- hero headline
- hero subheadline
- CTA labels
- section headings
- pricing labels
- feature names
- testimonial names and roles if clearly shown
- navigation labels
- footer labels when relevant

Visible text is part of the design system and must inform the implementation.

## Typography extraction

Do not stop at "the typography looks nice."

Extract and observe:

- size relationships
- weight relationships
- line count
- line height feel
- tracking feel
- serif versus sans behavior
- display versus body contrast
- section heading rhythm
- CTA text scale
- whether the type feels calm or aggressive

Do not flatten typography into a generic coded hierarchy.

## Spacing extraction

Analyze spacing deliberately.

Inspect:

- distance between headline and subheadline
- distance between text and buttons
- distance between cards
- section top and bottom spacing
- side gutters
- card padding
- image-to-text distance
- navigation spacing
- CTA block spacing
- overall cadence across sections

The goal is not exact pixel OCR.
The goal is faithful spacing logic.

## Button and component extraction

Buttons and components must be analyzed, not guessed.

Inspect:

- button size
- button shape
- button radius
- fill versus outline behavior
- icon usage
- hover-implied mood
- primary versus secondary hierarchy
- card structure
- badge usage
- dividers
- shadows
- borders
- pill logic
- input styling if present

## Color extraction

Actively extract the color system from the image.

Inspect:

- background color
- panel colors
- accent colors
- button fills
- text color hierarchy
- border color logic
- shadow color mood
- image tint or grade
- gradient restraint or intensity

The implementation should preserve the original color logic as closely as reasonably possible.
