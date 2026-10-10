---
name: pr-review
description: Review a GitHub pull request and write a full, evidence-based Markdown report; never post GitHub comments or edit source.
---

Review a pull request and write the report to `PR_REVIEW.md` at the repository root. This command is report-only: do not post or reply on GitHub, edit source or tests, or change branches.

## Target

`$ARGUMENTS` is an optional pull-request number or URL. With no argument, get the pull request for the current branch via `gh pr view --json number,title,url,headRefName,baseRefName`. With an argument, use `gh pr view <arg> --json number,title,url,headRefName,baseRefName` and compare its `headRefName` with `git branch --show-current`. If they differ, stop and tell the user to check out the PR first; never switch branches automatically. Stop if no pull request is available.

Use the caller's existing `gh` authentication. Do not request, print, or store credentials.

## Review

1. Read the PR description, changed files, diff, linked task or issue, and GitHub CI results when available. Use `gh pr checks <number>` for CI status. If task text or acceptance criteria cannot be accessed, continue and mark acceptance-criteria coverage `UNVERIFIED`; do not infer requirements.
2. Read the full relevant implementation, callers, configuration, and tests. Review the change in context, not from the diff alone. Trace suspected problems to concrete code or test evidence.
3. Load the `code-review` and `code-research` skills. Dispatch the built-in `reviewer` and `security-reviewer` in parallel. Reconcile their findings with your own evidence, remove duplicates, and omit speculation.
4. Review correctness and regressions, every available acceptance criterion, unhandled edge cases, security and privacy, performance, scope, test adequacy, maintainability, and style. Include valid low-impact suggestions too, but keep their severity low and distinguish them from defects.
5. Do not run local tests. Use available GitHub CI/check results as evidence; if unavailable, say so. Never imply that unrun tests passed.

## Severity

- **Critical** — credible risk of major outage, data loss, or severe security/privacy harm.
- **High** — major user-visible failure, security issue, or important acceptance criterion not met.
- **Medium** — meaningful defect, unhandled edge case, regression risk, or partial acceptance gap.
- **Low** — limited-impact maintainability, readability, or style issue.

Base severity on concrete impact. Do not inflate style or preference findings.

## Write `PR_REVIEW.md`

Overwrite the existing report on every run. Do not create or modify any other repository file.

Write readable Markdown with:

1. **Header** — PR title linked to the PR, number, head and base branches, and review date.
2. **Summary** — concise overall assessment and counts by severity. Say clearly when no findings were found.
3. **Acceptance criteria** — one row per criterion, with status `MET`, `PARTIAL`, `NOT MET`, or `UNVERIFIED`, plus evidence or the reason it could not be checked. If no criteria are available, add one `UNVERIFIED` row explaining that. Do not invent missing criteria.
4. **Findings** — a summary table with ID, severity, category, and exact `file:line`, followed by one section per finding. Each section must state:
   - **Evidence** — the observed code, behavior, or test and exact location.
   - **Impact** — what can go wrong for a user or the task.
   - **Recommendation** — the smallest concrete correction or next step.
   - **Suggested code** — include a concise snippet only when the fix is clear and supported by context. For broader or uncertain changes, give concrete steps and the relevant trade-off instead of inventing code.
5. **CI and checks** — available GitHub CI status and links; state that local tests were not run by this command.

Keep findings actionable and understandable to a reader unfamiliar with the code. Separate confirmed defects from risks and suggestions. Use exact paths and line numbers; support every claim with evidence. Do not write proposed findings as GitHub comment text.

## Never

Post or reply on GitHub, create a GitHub review, approve or request changes, resolve threads, edit source or tests, run local tests, commit, push, create or switch branches, or write files other than `PR_REVIEW.md`.
