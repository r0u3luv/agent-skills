---
name: code-review
description: Use when reviewing code changes for bugs, regressions, risk, and missing tests before merge.
---

# Code Review

Focus on issues that could affect correctness, production behavior, security, data integrity, or maintainability.

## Workflow

1. Inspect the diff and nearby code.
2. Identify behavior changes and affected contracts.
3. Check for missing or weak tests proportional to the risk.
4. Report actionable findings first, ordered by severity.
5. Include a short summary only after findings.

## Output

Use this structure:

- Findings
- Open questions or assumptions
- Brief summary
- Verification gaps

If there are no findings, say so clearly and mention any residual risk.

## References

Read `references/review-checklist.md` when the change touches shared infrastructure, auth, billing, data migrations, concurrency, or public APIs.

