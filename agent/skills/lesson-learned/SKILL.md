---
name: lesson-learned
description: "Extract evidence-backed engineering lessons when the user asks 'what did we learn?', 'what can I learn from this fix?', 'reflect on these changes', or 'what should we do differently next time?'. Use the named change or current conversation, not automatic post-task memory capture, a general code review, or an architecture survey."
license: MIT
metadata:
  source: https://github.com/softaworks/agent-toolkit/blob/3027f20f3181758385a1bb8c022d4041dfb4de84/skills/lesson-learned/SKILL.md
  source_commit: 3027f20f3181758385a1bb8c022d4041dfb4de84
  adaptation: OMP passive skill; request-scoped evidence; no default Git-history sweep
---

# Lessons from actual work

Use the user's actual change as evidence, not an occasion for generic advice.

## Workflow

1. Resolve the requested scope from the named fix, supplied diff or current conversation. Read the relevant implementation and observed outcomes. Use a bounded read-only Git diff/history only when the user-selected scope needs it; do not default to the last five commits or read unrelated session history.
2. Identify the most instructive mechanism: a mistaken assumption, an invariant, a boundary, an effective diagnostic, or a consequential trade-off. Separate demonstrated outcomes from inference. Do not claim that an unrun check or an edit proved the fix.
3. Explain the lesson with concrete evidence:
   - **What happened:** cite the relevant file/line or observed result.
   - **Why it mattered:** explain the mechanism and the constraint it exposed.
   - **Next time:** give a reusable decision or diagnostic action, scoped to the same conditions.
4. Add another lesson only when it is distinct and equally grounded. Straightforward housekeeping does not need a forced lesson. Avoid blame, invented intent, unrequested redesigns or claims of measurable improvement without evidence.

## Persistence

Return the lesson in the conversation. Do not automatically write memory, change skills/rules, create an ADR or commit anything. If the user explicitly asks to preserve a lesson, use `writing-for-agents` for a reusable procedure and `documentation-and-adrs` for a consequential decision or durable constraint. Do not persist task-specific data as a global preference.

## Completion

Every lesson has evidence, a coherent mechanism and a scoped action. Unknown outcomes remain unknown. This workflow does not authorize tests, retries, fixes or history collection beyond the request.

## Source

Adapted from Softaworks lesson-learned at the pinned revision above. See LICENSE and provenance.json. The OMP version removes mandatory principle catalogs, default history sweeps and fixed lesson-count quotas.
