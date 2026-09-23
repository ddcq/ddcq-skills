---
name: prepare-pr
description: Prepare and validate a code change before opening a pull request. Use when Claude Code should check scope, tests, documentation, risk, commit hygiene, and PR readiness without creating or sending the PR unless explicitly asked.
---

# Prepare PR

Inspect repository contribution rules, branch status, diff, commit history, changed files, and relevant CI configuration. Confirm that the diff matches the requested scope and does not include accidental generated files, secrets, debug code, unrelated formatting, or incomplete migrations.

Run the narrowest relevant checks, then broader checks when practical. Verify tests, types, lint, build, documentation, release notes, feature flags, backwards compatibility, observability, and rollback considerations.

Return:

```text
PR readiness: READY | READY WITH FOLLOW-UP | NOT READY

Scope:
- ...

Checks:
- command — result

Blocking issues:
- ...

PR summary:
- Problem:
- Solution:
- Risks:
- Validation:
```

Do not commit, push, open a PR, or alter files unless explicitly requested.
