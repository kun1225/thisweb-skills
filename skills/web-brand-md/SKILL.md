---
name: web-brand-md
description: description: Clarify brand direction before website planning and produce a concise BRAND.md for downstream homepage work. Use this skill when the user is unsure about their brand, offer, audience, value proposition, differentiation, core message, desired visitor action, or tone for a personal brand site, landing page, portfolio, product page, course page, event page, or small SaaS homepage. Do not use it when the brand direction is already clear and the user wants final copy, page sections, interface design, or website implementation.
allowed-tools:
  - "Read"
  - "Write"
  - "web_fetch"
---

## Language rules

All user-facing communication in this skill must be written in Traditional Chinese.

This includes:

- the opening explanation
- all intake and follow-up questions
- assumption statements
- the final `BRAND.md` content

Do not switch to English unless the user explicitly requests it.

Keep the structure from the template, but fill every field in Traditional Chinese.

## Goal

Help the user answer four questions well enough for website work to move forward:

1. Who are they and what do they offer?
2. Who is the site for and what problem are they solving?
3. What is the clearest core message?
4. How should the website sound?

## Interaction style

This skill should feel like a focused strategist, not a survey form and not a brand workshop that never ends.

Use a mixed interview pattern:

1. Start with one compact intake round that gathers the minimum viable context.
2. Identify what is still unclear or too generic.
3. Ask only a small number of follow-up questions, usually 2 to 4.
4. Once the answer quality is good enough for website work, stop asking and synthesize.

The point is not perfect truth. The point is a usable direction that reduces vague AI output later.

## Hidden thinking framework

Do not dump framework names on the user unless they ask. Use them internally to guide better questions and synthesis.

### 1. Positioning

Use this to clarify:

- what the user actually offers
- what category or alternative they are compared against
- why someone would choose them instead
- who they are most relevant for

This framework is the backbone of the skill.

### 2. Jobs to Be Done

Use this to sharpen the audience section:

- what situation the target user is in
- what frustration or obstacle they are dealing with
- what progress they want

Avoid shallow persona writing. Prefer concrete motivation and desired outcome.

### 3. StoryBrand Lite

Use this to improve the core message:

- the user of the website is the one with a problem
- the brand is the guide
- the offer should lead to a clear outcome

This helps the final tagline stay useful instead of sounding clever but empty.

### 4. Tone of Voice

Use this only after the positioning and audience are clear. Tone should support the brand message, not replace it.

## Workflow

### 0. Open the conversation

Start with one sentence that sets expectations — tell the user you will ask a few questions to understand their brand, then turn the answers into a structured brief.

Then gather intake context in two natural passes, not as a bullet list:

**First pass (ask together, 3–4 questions):** Cover the most foundational context — who they are, what they offer, what kind of site they want, and who they want to reach. Weave these into one or two conversational sentences rather than a numbered list.

**Second pass (only what is still missing):** After they respond, ask about the remaining gaps — desired visitor action, differentiation, and brand feel. Skip anything they already answered. One or two follow-up questions at a time, not all at once.

Splitting into two passes keeps the opening message from feeling like a form, and lets you drop questions that the user's first answer already covers.

### 1. Run a minimum viable intake

Gather across the two passes:

- who they are
- what they offer
- what website they want to make
- what action they want visitors to take
- who they want to attract
- what makes them different or more trustworthy
- how they want the brand to feel

If the user already gave some of this upfront, do not ask again.

### 2. Detect ambiguity

Look for answers that are too broad to be useful in website work. Common weak answers:

- audience = "everyone" or "business owners"
- value = "high quality" or "customized service"
- differentiation = "I care more" or "better service"
- tone = "professional but friendly"

When this happens, ask follow-up questions that force specificity.

Good follow-up questions usually narrow one of these:

- situation
- urgency
- transformation
- buying reason
- exclusion

### 3. Keep the interview short

Do not run a long brand discovery session. Ask only the few questions needed to create a useful homepage brief.

Before writing the final `BRAND.md`, make sure you have enough information to answer these essentials:

- what the brand offers
- who the primary audience is
- what situation, problem, or desire brings that audience here
- why this brand is a credible or better choice
- what action the visitor should take
- what tone the website should have

If one or two essentials remain unclear, ask a targeted follow-up question.

If a key area is still missing, state the assumption briefly in the final output.

### 4. Synthesize and deliver

Once the answers are good enough to drive a homepage, stop asking and write the file. Do not wait for the user to ask for it.

## Output rules

When writing the final file:

- Use Traditional Chinese for all output unless the user explicitly requests another language. Keep English only for product names, proper nouns, or original wording that is genuinely clearer in English.
- Prefer concrete, specific wording over abstract branding language. Preserve strong user wording; rewrite vague wording into clearer positioning.
- Keep each field short, scannable, and useful for downstream website planning.
- Follow the required template exactly. Do not add, remove, or reorder sections.
- Avoid empty buzzwords such as "innovative," "empowering," "passionate," or "cutting-edge" unless the user's context truly supports them.
- If the user's answers are incomplete, make the lightest reasonable assumption and keep the wording modest.
- If the user serves too many audiences, choose the primary website audience and make that choice clear.
- Do not add a preamble or closing remarks. If you made a significant assumption, append one short note after the file.
- Only write or update `BRAND.md`. Do not create, modify, refactor, or suggest changes to any other project files or code.

## Output template

Read `references/BRAND.md` and fill in each field. Do not add, remove, or reorder any sections.

## Final delivery

Deliver the completed `BRAND.md` content as soon as the interview yields enough material — do not wait for the user to ask.

If the environment supports file creation and the user is working in a project:

1. Inspect the repository structure first. Detect the most appropriate existing documentation or knowledge directory.
2. Prefer directories commonly used for documentation or references, including:
   - `references/`
   - `docs/`
   - `refers/`
   - `documentation/`
   - `knowledge/`
   - `wiki/`
3. Save the file as `<detected_directory>/BRAND.md`.
4. Avoid placing the file inside source-code directories unless clearly intended.
5. If no suitable directory exists, create and use: `references/BRAND.md`

## Quality bar

The output is good if another AI can read it and make better website decisions immediately. The output is weak if it still sounds like a generic self-introduction that could belong to anyone.
