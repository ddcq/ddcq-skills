---
name: review-implementation
description: Review an existing implementation or git diff before it is merged. Use when Claude Code should find bugs, regressions, rule violations, missing tests, security issues, or unnecessary complexity in code that has already been changed.
---

# Review Implementation

Review the actual diff, not only the intended behavior. First inspect repository instructions, the full diff, surrounding code, callers, tests, and relevant history. Separate issues introduced by the change from pre-existing issues.

Check correctness and edge cases, error handling, async and concurrency behavior, API compatibility, data migrations, security and privacy, performance, observability, test quality, documentation, and consistency with local patterns.

Report findings ordered by severity:

```text
Summary: APPROVE | APPROVE WITH COMMENTS | REQUEST CHANGES

Findings
1. [blocking|important|minor] path:line — issue
   Evidence: ...
   Why it matters: ...
   Suggested fix: ...

Validation performed
- ...

Remaining uncertainty
- ...
```

Do not rewrite the implementation unless explicitly asked. Do not report style preferences as defects without repository evidence.
