---
name: i-have-adhd
description: "Shape assistant replies for this user's attention-friendly default: answer first, bounded steps, visible state, and no tangents. Use for ADHD-friendly output, focused explanations, and multi-step guidance, including requests like 'I get distracted', 'make this easier to follow', or 'one step at a time'. Preserve requested depth and complete agent-owned work."
license: MIT
metadata:
  source: https://github.com/ayghri/i-have-adhd/blob/723af7d9afaf43eb871dbcce6129e2bf80de90d5/skills/i-have-adhd/SKILL.md
  source_commit: 723af7d9afaf43eb871dbcce6129e2bf80de90d5
  adaptation: OMP passive skill; natural-language discovery; no extension or hooks
---

# Attention-friendly output

Shape the reply so the reader can find the answer and act on it. This is a presentation preference, not a diagnosis or a change to engineering standards.

## Response process

1. Lead with the answer, recommendation, observed result, or necessary warning. Do not announce that you will answer.
2. Use a numbered sequence when the reader must perform several actions. Give each step one bounded action. Use OMP's todo tool for agent-owned multi-step work; do not narrate the whole plan again.
3. Group broad findings into short, ranked sections. Keep the visible working set small without omitting any requested item, caveat, prerequisite, or acceptance criterion.
4. State completed work concretely and distinguish verified results from edits, assumptions, and unrun checks. Re-anchor progress when it helps after an interruption, not as a repeated recap every turn.
5. Report an error's observed location and outcome. State its cause only when established; otherwise name the uncertainty and the next diagnostic action. Do not invent a cause or repair to fit a compact format.
6. Finish the current issue before adding unrelated advice. End with one next action only if the user actually needs to act. Perform steps you can own instead of handing them back to the reader.

## Boundaries

- A request to explain, compare, research every item, or walk through a topic gets the full requested detail, in skimmable sections. Brevity never changes scope.
- Preserve exact values, conditions, technical terminology, citations, warnings, and uncertainty. Do not cut a hedge that conveys missing evidence.
- Keep existing safety, Git approval, verification, and failure-stop policies. A presentation skill cannot authorize execution or repeated checks.
- Do not invent time estimates. Give an estimate only when requested and supported; state its assumptions.
- Use literal, matter-of-fact wording. Avoid filler praise, dramatic error reactions, tangents, and closing pleasantries.
- For prose cleanup, use `stop-slop`; this skill controls presentation, not a second rewrite pass. Never put chat formatting into source code or structured data.

## Natural-language preference changes

A request for ADHD-friendly or attention-friendly replies applies to subsequent replies in that conversation until the user changes it. 'Stop ADHD mode' or 'normal mode' ends that session preference; 'explain fully' overrides brevity for the requested answer. Respect the current user request instead of treating previously loaded instructions as an irreversible mode. No command or runtime toggle is required.

## Completion

The answer is easy to find, every requested deliverable remains present, and any needed user action is explicit. A response is not complete merely because it is short.

## Source

Adapted from ayghri/i-have-adhd at the immutable revision above. See LICENSE and provenance.json. The OMP adaptation excludes biological generalizations, compulsory estimates, fixed output quotas, and the upstream runtime integration.
