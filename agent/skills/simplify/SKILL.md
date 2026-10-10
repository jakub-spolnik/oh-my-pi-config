---
name: simplify
description: Simplify or refactor code for readability and maintainability while preserving observable behavior. Use after the behavior is understood; broad codebase overhaul requests follow the global balanced-control policy before implementation.
---

# Code Simplification

## Overview

Simplify code by reducing complexity while preserving exact behavior. The goal is not fewer lines — it's code that is easier to read, understand, modify, and debug. Every simplification must pass a simple test: "Would a new team member understand this faster than the original?"

Follow RULES.md's balanced overhaul control: clear scoped refactors may proceed; broad overhauls begin with a proposal and target agreement. Do not invent opportunities in already clear code.

## When to Use

- After a feature is working and tests pass, but the implementation feels heavier than it needs to be
- During code review when readability or complexity issues are flagged
- When you encounter deeply nested logic, long functions, or unclear names
- When refactoring code written under time pressure
- When consolidating related logic scattered across files
- After merging changes that introduced duplication or inconsistency

**When NOT to use:**

- Code is already clean and readable — don't simplify for the sake of it
- You don't understand what the code does yet — comprehend before you simplify
- The code is performance-critical and the "simpler" version would be measurably slower
- You're about to rewrite the module entirely — simplifying throwaway code wastes effort

## The Five Principles

### 1. Preserve Behavior Exactly

Don't change what the code does — only how it expresses it. All inputs, outputs, side effects, error behavior, and edge cases must remain identical. If you're not sure a simplification preserves behavior, don't make it.

Before every change, ask:

- Does this produce the same output for every input?
- Does this maintain the same error behavior?
- Does this preserve the same side effects and ordering?
- Do existing observable-contract tests still describe the preserved behavior? Do not rewrite assertions merely to accommodate a changed implementation; report unrun checks as unrun.

### 2. Follow Project Conventions

Simplification means making code more consistent with the codebase, not imposing external preferences.

Before simplifying:

1. Read `AGENTS.md` / project conventions
2. Study how neighboring code handles similar patterns
3. Match the project's style for imports, naming, function style, error handling, and type annotations

Simplification that breaks project consistency is not simplification — it's churn.

### 3. Prefer Clarity Over Cleverness

Explicit code is better than compact code when the compact version requires a mental pause to parse.

- Replace nested ternaries with readable control flow
- Replace dense inline transforms with named intermediate steps when they clarify intent
- Keep helpful names even if they cost a few extra lines

### 4. Maintain Balance

Watch for over-simplification:

- Don't inline away names that carry meaning
- Don't merge unrelated logic into one larger function
- Don't remove abstractions that serve testability or extensibility
- Don't optimize for line count over comprehension

### 5. Scope to What Changed

Default to simplifying recently modified code. Avoid unrelated drive-by refactors unless explicitly asked.

## Process

### Step 1: Understand Before Touching

Before changing or removing anything, understand why it exists.

Answer:

- What is this code's responsibility?
- What calls it? What does it call?
- What are the edge cases and error paths?
- Are there tests that define expected behavior?
- Why might it have been written this way?

If you can't answer these, read more context first.

### Step 2: Look for Simplification Opportunities

Signals:

- Deep nesting
- Long functions with mixed responsibilities
- Nested ternaries
- Boolean flag arguments
- Repeated conditionals
- Generic or misleading names
- Duplicated logic
- Dead code
- Wrappers or abstractions that add no value

### Step 3: Apply Changes Incrementally

Apply a coherent set of scoped simplifications incrementally, preserving behavior at each step through the understood contract and relevant source/test evidence.

Do not run tests after each edit. After the change is complete, perform the single end-of-change correctness self-review and, when warranted, the one narrow relevant check permitted by RULES.md. Skip command checks for small low-risk changes unless requested. On failure, stop validation and automatic repair; report the exact command and actual failure without retrying.

Separate refactoring from feature work whenever possible.

### Step 4: Verify the Result

After simplifying, confirm:

- The code is genuinely easier to understand
- The diff is clean and reviewable
- Project conventions still match
- No behavior, error handling, or side effects changed

## Guidance for This Repository

- Follow the repository's actual language, framework and architecture conventions; prefer straightforward expression over clever compression.
- Preserve existing runtime behavior, tests, and hooks
- Favor explicit names and smaller focused helpers when they improve readability
- Keep refactors tightly scoped to the task or review feedback

## Verification Checklist

- [ ] Observable behavior and public/persisted contracts are preserved; available evidence and unrun checks are distinguished.
- [ ] Verification followed the global one-check/failure-stop policy; no formatter or per-edit check sweep was run.
- [ ] No unrelated files were refactored
- [ ] No error handling was weakened or removed
- [ ] The result is simpler to review than the original
