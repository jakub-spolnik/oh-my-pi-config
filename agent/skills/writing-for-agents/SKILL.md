---
name: writing-for-agents
description: Write, revise, or explicitly audit/refactor agent-facing instructions such as skills, AGENTS.md, CLAUDE.md, project rules, and linked guidance. Use for instruction-authoring work, not incidental code tasks; for a skill's lifecycle, pair with skill-creator.
license: MIT
metadata:
  source: https://github.com/mattpocock/skills/tree/c55ee46073ed923f86ce59a5eb3b6d895095d1b7/skills/productivity/writing-for-agents
  source_commit: c55ee46073ed923f86ce59a5eb3b6d895095d1b7
  adaptation: OMP; integrated evidence-led audits, authoritative ownership, progressive disclosure, and knowledge-delta criteria
---

# Writing for Agents

Write agent-facing documents so the agent follows a reliable process rather than merely producing familiar-looking output.

When editing a skill, also read [SKILL-MECHANICS.md](./SKILL-MECHANICS.md).

## Routing and scope

Use this skill when the user asks to write, revise, audit, or refactor agent-facing instructions. An audit is scoped to the named files and their instruction links; do not start a broad instruction audit during unrelated coding or documentation work.

For creating, modifying, or explicitly evaluating a skill, use [skill-creator](../skill-creator/SKILL.md) for the skill lifecycle and this skill for instruction design. Keep OMP loading and metadata behavior grounded in [SKILL-MECHANICS.md](./SKILL-MECHANICS.md).

| Request | Route |
| --- | --- |
| “Turn this incident procedure into an OMP skill.” | `skill-creator` with this writing guidance |
| “Audit `AGENTS.md` for conflicting test rules and broken instruction links.” | This skill |
| “Review this Kotlin handler for a race condition.” | The relevant code-review/debugging skill, not an instruction-file audit |

## Explicit instruction audits and refactors

1. Bound the audit to the requested instruction files. Read their linked references and search for callers or duplicate copies before editing; do not infer content from filenames alone.
2. Record conflicts with exact source evidence. Resolve them from applicable authority, scope, explicit precedence, and repository evidence. Ask the user only when a material conflict remains unresolved after that analysis.
3. Keep one authoritative owner for each rule. Replace duplicates with precise pointers to the owner; preserve distinct scoped overrides when they are intentional.
4. Organize for progressive disclosure: universal instructions stay in the always-loaded entry point; branch-specific details load only through a pointer that names the matching task. Preserve important technical facts and constraints rather than deleting them to reach a target size or category count.
5. Read back the edited instructions and follow each pointer to confirm its target exists and still covers the promised branch.

## Context pointers

A context pointer names material outside the current context and states exactly when to load it. Skill descriptions and references in `AGENTS.md` are context pointers.

A useful pointer:

- starts with the capability or trigger;
- names each genuinely distinct branch that should load the target;
- omits identity and detail already available in the target;
- is strong enough that required material is not skipped.

Always-loaded pointers spend context on every turn. Keep them short and precise.

## Information hierarchy

Organize content by when the agent needs it:

1. **Steps** — ordered actions required for this workflow.
2. **Local reference** — rules needed by most branches.
3. **Disclosed reference** — branch-specific detail in a linked sibling file.

Keep common steps in the main document. Move large or branch-specific reference behind a precise pointer, and keep each concept's definition, rules, caveats, and authoritative owner together.

Split a document only when the split reduces context or prevents later steps from pulling attention away from the current step. Do not split merely to shorten files or meet line-count targets.

## Completion criteria

Every step needs a checkable finish condition. Prefer exhaustive criteria such as “every modified public symbol has a migration decision” over vague criteria such as “review the API.” For an audit, make each conclusion traceable to an instruction source, affected caller, or verified link.

A completion criterion must say:

- what evidence exists when the step is complete;
- which items must all be covered;
- which unresolved issue blocks advancing to the next step.

## Leading words

Use a compact, established term when it can anchor repeated behavior, such as *frontier*, *seam*, *red*, or *tracer bullet*. Define it once, then reuse the term instead of repeating its explanation. Prefer existing vocabulary over invented jargon.

Phrase instructions toward the desired behavior. Reserve prohibitions for hard safety boundaries and pair them with the positive action to take instead.

Keep one source of truth for each rule. Before retaining a sentence, ask whether it changes agent behavior compared with the default and whether the target audience has the relevant expertise. Preserve the knowledge delta: non-obvious decisions, domain-specific procedures, trade-offs, edge cases, and constraints that are not available from generic model knowledge.

Remove:

- duplicated rules;
- facts cheaply discoverable from configuration or code;
- stale workflow descriptions;
- speculative branches;
- generic advice without an observable effect.

Do not remove useful technical or factual detail just to make a file shorter. Do not impose fixed line, word, file, category, or score quotas; judge structure and detail by whether they improve routing, loading, and use.

Preserve unwritten conventions, reasons, safety constraints, and non-obvious completion criteria.

## Review checklist

- The description names the exact invocation branches and excludes realistic near-misses.
- Broad audits and refactors run only when requested and stay within the named scope.
- Steps are ordered and end in checkable, evidence-backed outcomes.
- Contradictions are resolved by authority, scope, precedence, and repository evidence; unresolved material conflicts are surfaced rather than guessed.
- Each rule has one authoritative location; pointers lead to existing, relevant files.
- Common and branch-specific guidance load at the right time without arbitrary size or category quotas.
- The document preserves useful expert and technical detail while removing redundant or generic filler.
- Repository configuration is referenced instead of copied.
- Safety requirements state both the prohibition and the correct alternative.
- Examples reinforce the contract rather than add a competing one.
