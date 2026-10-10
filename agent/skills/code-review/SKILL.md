---
name: code-review
description: >-
  Unified code review skill for giving reviews, adversarial review personas, and
  receiving review feedback. Use when reviewing code changes, PRs, or review comments.
  Covers correctness, architecture, security, performance, maintainability, test
  coverage, hostile review mindset, and technical response to feedback.
---

# Code Review

## Giving Reviews

### Goal

Produce technical, actionable review output. Never rubber-stamp.

### Review Workflow

1. Read the original requirement.
2. Read the plan, if any.
3. Read the tests.
4. Read the implementation in full context.
5. Decide if the change is correct, safe, and maintainable.

Review is read-only unless the user also requests implementation. Inspect relevant callers, contracts and configuration; use LSP references when available. Findings require exact evidence, a reachable consequence and a smallest defensible correction. A review with no actionable findings is valid.

Follow RULES.md's execution policy: use existing evidence, distinguish unrun checks, and do not start a test/build/lint sweep. Any authorized narrow check is shared across the change; its failure stops validation and automatic repair. Use one coherent end-of-change review, not repeated persona/model-verifier loops.

### Review Checklist

#### Correctness

- Does it satisfy the request?
- Does it match the plan?
- What actual test/build results are available, and which checks remain unrun or uncertain?
- Are edge cases handled?

#### Code Quality

- Is it readable and named well?
- Is there duplication that should be removed?
- Do cohesion, naming, nesting or scattered responsibility make the actual behavior harder to understand? Do not extract code solely to satisfy size metrics.
- Does it follow local idioms and patterns?

#### Architecture

- Are layers separated cleanly?
- Are dependencies minimal and justified?
- Are files in the right place?
- Does it match established project conventions?

#### Security

- Are inputs validated?
- Are secrets or PII exposed?
- Are auth/access checks correct?
- Do errors leak internals?

#### Performance

- Any N+1s or repeated work in loops?
- Are queries/indexes reasonable?
- Are resources cleaned up?
- Any unnecessary allocations or recomputation?

#### Maintainability

- Any dead code or magic values?
- Is error handling explicit?
- Is logging useful and not noisy?
- Any unsafe casts or suppressions?

#### Test Coverage

- Are changed paths tested?
- Are error paths tested, not just happy paths?
- Are tests behavior-focused?
- Do test helpers keep setups simple?

### Bug Fix Review Additions

- Does the fix address root cause?
- Is regression risk controlled?
- Is the scope minimal?
- Is there a regression test?

### Severity

- **CRITICAL**: security breach, data loss, outage
- **HIGH**: major bug, architectural violation, serious perf issue
- **MEDIUM**: maintainability issue or missing edge case
- **LOW**: minor suggestion or style preference

### Output Format

Use one of these:

```markdown
## Review Verdict: APPROVE ✓
### Summary
### Quality Assessment
### Highlights
### Minor Suggestions
```

```markdown
## Review Verdict: REQUEST_CHANGES ✗
### Summary
### Issues Found
#### Issue 1: [title] — [severity]
**Category:** ...
**Location:** `path:line`
**Problem:** ...
**Impact:** ...
**Fix:** ...
```

### Adversarial Personas

Use the relevant perspectives below within one review pass, not as compulsory subagents or issue quotas. Never manufacture a defect or fragile assumption to make a perspective produce a finding.

#### 1) Saboteur

Mindset: break it in production.

Look for:

- Unvalidated input
- State inconsistency
- Concurrency hazards
- Bad failure handling
- Bad assumptions about data size/shape/availability
- Off-by-one / null / overflow / resource leaks

Questions:

- What is the worst input?
- What if this call fails or times out?
- What if this runs twice or concurrently?
- What if neither branch is correct?

#### 2) New Hire

Mindset: understand and modify it in 6 months with no context.

Look for:

- Confusing names
- Logic spread across too many files
- Magic constants
- Multi-purpose functions
- Hidden knowledge in code
- Tests that assert internals instead of behavior

Questions:

- Can the intent be understood from the function signature and body?
- How many files are needed to trace one path?
- Where would a new contributor add a similar feature?

#### 3) Security Auditor

Mindset: an attacker will hit this code.

Look for:

- Injection
- Broken auth
- Missing access control
- Sensitive data exposure
- Insecure defaults
- Dependency risk
- Secrets in code or comments

Questions:

- What trust boundaries are crossed?
- Is input validated and output sanitized?
- Can privileges be escalated?
- Does this add attack surface?

### Adversarial Rules

- If no actionable defect is supported, say so and report any remaining uncertainty; do not force findings.
- State supported consequences directly, without inflated certainty or severity.
- Do not review only changed lines.
- Deduplicate repeated findings.
- Assign severity from impact, reachability and evidence, not the number of perspectives that noticed it.

### Review Anti-Patterns

- Vague concerns instead of concrete fixes
- Cosmetic-only findings while missing real bugs
- Approving despite major issues
- Requesting changes without saying how to fix them

## Receiving Reviews

### Goal

Verify review feedback before acting on it. Technical correctness over performative agreement.

### Response Pattern

1. Read the feedback fully.
2. Restate the requirement in your own words.
3. Verify against the codebase.
4. Evaluate whether it is correct here.
5. Respond technically.
6. Implement the authorized fixes within scope, then use the shared end-of-change review and permitted narrow check; do not test or format after every fix.

### Rules

- Do not say “you’re absolutely right.”
- Do not say “great point.”
- Do not promise implementation before verification.
- Resolve unclear facts from code and configuration first; ask only when a material intent or trade-off remains undecided.
- If wrong, push back with facts and tests.
- If correct, just fix it and state what changed.

### When Feedback Is Unclear

- Resolve missing facts from the code and configuration before questioning the user.
- Pause only the affected ambiguous changes; clear, independent fixes may proceed when already authorized.
- Ask only about remaining intent, scope or trade-offs that evidence cannot settle.

### When to Push Back

Push back if the suggestion:

- breaks behavior
- conflicts with existing decisions
- violates YAGNI
- is technically wrong for this stack
- cannot be verified yet

Use evidence, not defensiveness.

### Implementation Order

1. Blocking issues
2. Simple fixes
3. Complex refactors
4. Verify the completed changes proportionally under RULES.md's shared one-check/failure-stop policy.
5. Report observed results and unverified regression risks without claiming unrun checks passed.

### GitHub Replies

Reply in the inline thread, not as a top-level PR comment.

### Common Mistakes

- Performative agreement
- Blind implementation
- Claiming a batch of changes is verified without evidence, or running unapproved checks/retries
- Proceeding while unclear
- Avoiding justified pushback

### Bottom Line

Review feedback is input to verify, not an order to obey.
