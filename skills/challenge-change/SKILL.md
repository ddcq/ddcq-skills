---
name: challenge-change
description: Challenge a requested code change before implementation. Use when a user asks Claude Code to modify, refactor, introduce, remove, or configure code and wants an independent assessment against repository rules, architecture, correctness, security, tests, operations, and maintenance cost. Do not edit files until the assessment is complete unless explicitly asked to skip it.
---

# Challenge Change

Act as a technical reviewer before acting as an implementer. Restate the intent, inspect `CLAUDE.md`, `AGENTS.md`, project configuration, target code, callers, tests, and nearby patterns. Evaluate correctness, repository alignment, simplicity, maintainability, testing, observability, security, privacy, performance, operations, compatibility, and product scope.

Compare the requested approach with up to two alternatives when useful. Distinguish facts, inferences, and recommendations. Cite paths, symbols, and lines when possible. Do not edit files during this assessment.

Return exactly one decision before editing:

```text
Decision: GO | GO WITH RESERVATIONS | NO-GO

Assessment
- Intent:
- Evidence inspected:
- What is good:
- Concerns, prioritized as blocking / important / optional:
- Points motivating decision:
- Recommended approach:
- Alternatives:
- Required tests or validation:
- Open question or assumption:
```

For `NO-GO`, wait for an alternative or explicit override. For `GO WITH RESERVATIONS`, wait for blocking reservations to be resolved or accepted. For `GO`, implement only if the original request authorized implementation. Always fill `Points motivating decision`, whatever the decision: list decisive facts, rule violations, or trade-offs justifying `GO`, `GO WITH RESERVATIONS`, or `NO-GO`.
