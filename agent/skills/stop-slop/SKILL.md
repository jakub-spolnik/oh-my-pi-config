---
name: stop-slop
description: Use when drafting or editing prose, including technical explanations, reports, emails, and documentation, to make it direct and natural or remove formulaic AI-like phrasing. Also use for requests such as “remove AI slop,” “make this less AI-sounding,” or “cut filler.” Use humanizer for explicitly named humanizer or naturalize-documentation requests; use simple-english for technical explanations requested in plain English.
license: MIT
metadata:
  source: https://github.com/hardikpandya/stop-slop
  source_commit: 8da1f030185bdfe8471220585162991eaeb970e9
  adaptation: OMP; contextual prose editing with strict content preservation
---

# Stop Slop

Draft or revise the prose the user requested. Prefer direct, natural wording and remove formulaic filler when it gets in the way. The patterns below are prompts for judgment, not a checklist to apply mechanically.

## Edit in context

- Cut throat-clearing openers, empty emphasis, repeated transitions, and chatbot residue when they add no meaning.
- Replace inflated praise, sales language, or vague claims of importance only when the source already supports a clearer statement. Do not manufacture specifics.
- Notice repeated sentence shapes, stock contrasts, staged rhetorical questions, dramatic fragments, and forced lists. Change them only when they make this text less clear or less natural; valid contrast, questions, fragments, and lists can stay.
- Prefer a clear active subject when the source identifies the actor and naming them improves clarity. Keep passive voice when the actor is unknown, irrelevant, or conventional for the document.
- Preserve the writer's voice, audience, document conventions, and useful repetition. Vary rhythm by ear, not by quotas.

No word or punctuation pattern is a blanket ban. In particular, do not remove adverbs, passive voice, hedges, em dashes, Wh- sentence openings, or list items just because they match a pattern. A pattern matters only when it is doing empty or formulaic work in context.

## Preserve content and scope

- Preserve every factual claim, number, name, date, range, identifier, attribution, and citation, along with its scope and certainty.
- Preserve warnings, caveats, uncertainty, modal strength, and requirements. Do not weaken or strengthen words such as `MUST`, `REQUIRED`, `SHOULD`, `RECOMMENDED`, `MAY`, `OPTIONAL`, `NEVER`, or `AVOID`.
- Keep code, commands, quoted errors, links and destinations, citations, identifiers, frontmatter, tables, and structured data unchanged unless the user explicitly asks to edit them. Do not alter code or formatting-sensitive text as a side effect of prose work.
- Never invent people, actors, causes, examples, attribution, or other details to make prose sound specific. If the source leaves something unknown, keep it unknown.
- Edit only the text and scope the user selected. Do not cut useful information merely to make the result shorter.

## Workflow

1. Read the supplied text and nearby context. Identify the requested scope, audience, voice, and any protected structured content.
2. Draft or revise the prose in one focused pass, using only patterns that actually reduce clarity or naturalness here.
3. Compare the result with the source. Confirm that every claim, quantity, qualification, warning, uncertainty, identifier, quote, and link remains intact, and that protected content is unchanged.
4. Return the requested artifact in the requested form. Do not add a score, checklist, or process commentary unless asked.

Use this as the principal prose-editing skill for ordinary anti-slop and drafting requests. Do not stack it with a second full rewrite from `humanizer`; use `humanizer` instead when the user explicitly names it or asks to humanize/naturalize existing documentation. Use `simple-english` when the request is to explain technical material in plain English.
