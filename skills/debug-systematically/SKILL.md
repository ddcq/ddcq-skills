---
name: debug-systematically
description: Investigate software bugs systematically from symptoms to verified root cause. Use when Claude Code is asked to debug an error, regression, flaky test, incident, performance problem, or unexpected behavior.
---

# Debug Systematically

Do not jump directly to a patch. Establish the observed symptom, expected behavior, affected scope, timeline, reproducibility, and known constraints. Inspect logs, traces, configuration, recent changes, inputs, and the smallest relevant code path.

Maintain explicit hypotheses:

```text
Hypothesis | Evidence for | Evidence against | Next experiment | Status
```

Prefer experiments that distinguish hypotheses. Reproduce before changing code when practical. Trace the data and control flow to the earliest point where reality diverges from expectation. Identify the root cause separately from contributing factors and mitigations.

Before proposing a fix, state:

- root cause and evidence;
- why the fix addresses the cause;
- affected edge cases;
- regression tests;
- observability or rollback needs;
- unresolved uncertainty.

Do not claim a root cause from correlation alone. If evidence is insufficient, say what would verify it.
