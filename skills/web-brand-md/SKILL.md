---
name: web-brand-md
description: Clarify a user's brand direction before website structure, copywriting, or visual design begins, then produce a concise `BRAND.md` that downstream AI can use for homepage decisions. Use this skill when the user is still unclear about their brand direction, audience, value proposition, differentiation, core message, or tone for a personal brand site, landing page, portfolio, product page, course page, event page, or small SaaS homepage. Also use it when the user says they do not know how to describe their brand, offer, target audience, or core message yet, even if they do not explicitly ask for a "brand guideline." Do not use this skill when the brand foundations are already clear and the user is explicitly asking you to write final copy, build page sections, design the interface, or implement the website.
allowed-tools:
  - "Read"
  - "Write"
  - "web_fetch"
---

# Website brand guideline

This skill is for the stage before website structure and copy polish. Its job is to turn fuzzy business context into a compact brand brief that another AI step can reliably use.

The output is intentionally minimal. Do not expand it into a full brand strategy deck. Do not add homepage sections, full copywriting, wireframes, or design systems unless the user explicitly asks for them.

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

Then convert the answers into a `BRAND.md` file using the template in `references/BRAND.md`.

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

Do not keep digging once the material is strong enough to drive a homepage. If the user is busy, uncertain, or in workshop mode, make a reasonable synthesis instead of demanding exhaustive detail.

If a key area remains missing, state the assumption briefly before the final output.

### 4. Synthesize and deliver

Once the answers are good enough to drive a homepage, stop asking and write the file. Do not wait for the user to ask for it.

## Output rules

When writing the final file:

- Use Traditional Chinese for all output.
- Prefer concrete wording over abstract branding language.
- Keep each field short enough to be scannable.
- Write for downstream AI and website planning, not for executives.
- Preserve the user's language when it is strong and specific; rewrite vague wording into clearer positioning when it is not.
- Do not add sections outside the required template.
- Do not use empty buzzwords such as "innovative," "empowering," "passionate," or "cutting-edge" unless the user's context truly requires them.
- Do not mix Chinese and English unless a product name, proper noun, or original user wording is genuinely clearer in English.
- If the user provides source material in another language, still deliver the final result in Traditional Chinese unless the user explicitly asks for a different output language.
- If the user's answers are incomplete, make the lightest reasonable assumption and keep the wording modest.
- If the user serves too many audiences, pick the primary one for the website and reflect that clearly.
- Do not add a preamble or closing remarks. If you made a significant assumption, append one short line after the file noting it.

## Output template

Read `references/BRAND.md` and fill in each field. Do not add, remove, or reorder any sections.

## Final delivery

Deliver the completed `BRAND.md` content as soon as the interview yields enough material — do not wait for the user to ask.

If the environment supports file creation and the user is working in a project, save the result as `BRAND.md`.

## Quality bar

The output is good if another AI can read it and make better website decisions immediately. The output is weak if it still sounds like a generic self-introduction that could belong to anyone.
