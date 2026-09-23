# Claude Dev Skills

A collection of Claude Code skills that encourage deliberate engineering decisions before and after code changes.
These skills are designed as lightweight, evidence-based engineering gates.
They do not require hooks, external services, additional model calls, or automatic repository mutations.

## Skills

| Skill | Positioning |
|---|---|
| `challenge-change` | Evaluates whether a requested change should be implemented before planning or editing |
| `review-implementation` | Performs a compact, non-mutating review of an existing diff |
| `debug-systematically` | Provides a concise, hypothesis-driven debugging workflow |
| `explain-architecture` | Explains verified execution paths, boundaries, and invariants |
| `prepare-pr` | Checks PR readiness without committing, pushing, or opening a PR |
| `security-review` | Provides an explicit, on-demand threat review without hooks or automatic fixes |

For detailed comparisons with similar public skills and plugins, see [`docs/comparisons.md`](docs/comparisons.md).

## Install for local testing

```bash
claude --plugin-dir .
```

Then invoke a skill with its namespaced name, for example:

```text
/skills:challenge-change
```

## Install from a marketplace

```text
/plugin marketplace add ddcq/skills
/plugin install skills@skills-marketplace
```

Review the skill source before installing it. Skills influence Claude's behavior but are not a hard security boundary.

## Validate

```bash
claude plugin validate .
```

## License

MIT
