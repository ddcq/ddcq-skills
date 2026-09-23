# Comparison with Similar Claude Code Skills

This document explains how the skills in `ddcq-skills` compare with representative public Claude Code skills and plugins.

It is not an exhaustive inventory of every skill published online. The comparison focuses on established projects, official Anthropic plugins, and public implementations whose source code can be inspected.

## Project positioning

`ddcq-skills` provides lightweight, evidence-based engineering gates for Claude Code.

The collection intentionally favors:

- explicit decisions and structured outputs;
- inspection of repository-specific rules;
- non-mutating analysis before action;
- minimal dependencies;
- predictable behavior without hooks or additional services.

It is not intended to replace specialized multi-agent review systems, security scanners, static analysis, or human review.

## Summary

| Skill | Similar public projects | Main distinction |
|---|---|---|
| `challenge-change` | `review-plan`, Superpowers `writing-plans` | Evaluates whether a raw change request is appropriate before planning or editing |
| `review-implementation` | Anthropic `code-review`, `pr-review-toolkit`, Superpowers `requesting-code-review` | Compact, local, non-mutating review of an existing implementation |
| `debug-systematically` | Superpowers `systematic-debugging` | Concise hypothesis table and explicit incident, observability, and rollback concerns |
| `explain-architecture` | Claude Mods `explain` | Evidence-first explanation centered on real execution paths and failure boundaries |
| `prepare-pr` | Anthropic `commit-commands`, `pr-review-toolkit` | Readiness gate that does not commit, push, or create a pull request |
| `security-review` | Anthropic `security-guidance` | Explicit, on-demand threat review without hooks, automatic fixes, or extra model calls |

## `challenge-change`

### Similar public skills

- [`review-plan`](https://github.com/chrisblattman/claudeblattman/blob/main/skills/review-plan.md)
- [Superpowers `writing-plans`](https://github.com/obra/superpowers/blob/main/skills/writing-plans/SKILL.md)

### Shared behavior

These skills attempt to reduce implementation mistakes before code is changed. They inspect requirements, architecture, feasibility, scope, tests, and likely failure modes.

### How `challenge-change` differs

Most comparable skills expect a specification or implementation plan to exist already. `challenge-change` operates one step earlier: it evaluates the raw requested change itself.

It asks whether the proposed modification:

- solves the real problem rather than a symptom;
- fits repository rules and existing architecture;
- introduces unnecessary complexity or coupling;
- has a smaller or safer alternative;
- should be implemented at all.

It returns one explicit decision:

- `GO`;
- `GO WITH RESERVATIONS`;
- `NO-GO`.

It also prevents editing during the assessment and requires an explicit override when the recommendation is negative.

### Trade-offs

Public plan-review skills can provide deeper evaluation after a plan exists. Some use web research, specialist roles, independent subagents, or cross-model criticism. `challenge-change` does not currently provide those mechanisms.

### Recommended positioning

Use `challenge-change` before planning. Use a plan-writing or plan-review skill afterward when the decision is `GO`.

This is the most differentiated skill in the collection.

## `review-implementation`

### Similar public skills and plugins

- [Anthropic `code-review`](https://github.com/anthropics/claude-code/tree/main/plugins/code-review)
- [Anthropic `pr-review-toolkit`](https://github.com/anthropics/claude-code/blob/main/plugins/pr-review-toolkit/README.md)
- [Superpowers `requesting-code-review`](https://github.com/obra/superpowers/blob/main/skills/requesting-code-review/SKILL.md)
- [`learn-claude-code` code review skill](https://github.com/shareAI-lab/learn-claude-code/blob/main/skills/code-review/SKILL.md)

### Shared behavior

These tools review completed changes for correctness, maintainability, security, test coverage, and consistency with repository conventions.

### How `review-implementation` differs

`review-implementation` deliberately uses a single compact review workflow. It:

- reviews the actual diff and surrounding code;
- distinguishes issues introduced by the change from pre-existing issues;
- reads repository instructions before applying general conventions;
- requires path and line evidence where available;
- does not change the implementation unless explicitly requested;
- returns `APPROVE`, `APPROVE WITH COMMENTS`, or `REQUEST CHANGES`.

It does not require a GitHub pull request, GitHub CLI, external integration, or subagent orchestration.

### Trade-offs

Anthropic's review plugins provide substantially more automation. Depending on the plugin, they can use multiple specialized agents, confidence scoring, pull-request metadata, `git blame`, comment analysis, type-design review, test-gap analysis, and silent-failure detection.

The lightweight workflow is easier to inspect and adapt, but it has less independent verification and lower review depth.

### Recommended positioning

Present it as a portable, non-mutating diff gate rather than a replacement for a multi-agent PR-review system.

## `debug-systematically`

### Similar public skill

- [Superpowers `systematic-debugging`](https://github.com/obra/superpowers/blob/main/skills/systematic-debugging/SKILL.md)

### Shared behavior

The overlap is substantial. Both approaches require Claude to:

- investigate before proposing a fix;
- reproduce the failure when practical;
- inspect errors, logs, configuration, and recent changes;
- formulate and test hypotheses;
- identify the root cause instead of patching the symptom;
- verify the final correction.

### How `debug-systematically` differs

The skill is intentionally shorter and emphasizes an explicit hypothesis register:

```text
Hypothesis | Evidence for | Evidence against | Next experiment | Status
```

It also explicitly separates:

- root cause;
- contributing factors;
- temporary mitigation;
- permanent correction;
- observability and rollback requirements.

This makes it suitable for incident investigations and collaborative debugging notes.

### Trade-offs

Superpowers provides a more rigorous and mature process. It includes four strict phases, comparison with known-good implementations, a mandatory failing test, one-variable experiments, escalation after repeated failed fixes, and supporting techniques for root-cause tracing and defense in depth.

The current skill should not be presented as more comprehensive.

### Recommended positioning

Either describe it as a compact debugging workflow or specialize it further as `debug-production-incident`, focusing on distributed systems, environment differences, telemetry, mitigation, and rollback.

## `explain-architecture`

### Similar public skill

- [Claude Mods `explain`](https://github.com/0xDarkMatter/claude-mods/blob/main/skills/explain/SKILL.md)

### Shared behavior

Both skills inspect source code, dependencies, tests, project instructions, and execution flow to explain how a module or system works.

### How `explain-architecture` differs

The skill starts from a user-visible behavior or concrete entry point and follows the real execution path. It focuses on:

- component responsibilities;
- data and control flow;
- external boundaries;
- failure boundaries;
- invariants and repository conventions;
- tests and observability;
- extension points and risks;
- explicit separation between verified facts and inference.

It is intentionally tool-agnostic and has no required external binaries.

### Trade-offs

Claude Mods `explain` has a much broader feature set. It provides depth and focus modes, structural search, code statistics, language-specific agents, Mermaid diagrams, symbol lookup, dependency analysis, and optional persistence to architecture documentation.

`explain-architecture` is simpler and more portable, but less capable for large-scale exploration.

### Recommended positioning

Present it as an evidence-first architectural walkthrough. A narrower name such as `trace-request-flow` could further distinguish it from general-purpose explanation skills.

## `prepare-pr`

### Similar public plugins and skills

- [Anthropic `commit-commands`](https://github.com/anthropics/claude-code/blob/main/plugins/commit-commands/README.md)
- [Anthropic `pr-review-toolkit`](https://github.com/anthropics/claude-code/blob/main/plugins/pr-review-toolkit/README.md)
- Superpowers `finishing-a-development-branch`

### Shared behavior

These tools inspect branch changes, tests, repository state, and pull-request content before merge or publication.

### How `prepare-pr` differs

`prepare-pr` is a readiness gate rather than an automation command. It checks:

- whether the diff matches the intended scope;
- accidental generated files or unrelated formatting;
- debug code and possible secrets;
- tests, lint, type checks, and builds;
- documentation and release notes;
- migrations and backward compatibility;
- feature flags, telemetry, and rollback concerns;
- the proposed PR summary and test plan.

It returns `READY`, `READY WITH FOLLOW-UP`, or `NOT READY`.

Most importantly, it does not commit, push, create a branch, or open a pull request unless the user explicitly requests those actions.

### Trade-offs

Anthropic's `commit-commands` provides a more convenient end-to-end Git workflow, including staging, committing, pushing, branch creation, and pull-request creation. `pr-review-toolkit` offers deeper specialized review through several agents.

`prepare-pr` requires the user to perform or separately authorize those actions.

### Recommended positioning

Describe it as a non-mutating PR-readiness gate that can run before an automated commit-and-PR workflow.

## `security-review`

### Similar public plugin

- [Anthropic `security-guidance`](https://github.com/anthropics/claude-code/blob/main/plugins/security-guidance/README.md)

### Shared behavior

Both inspect changes for common security and privacy risks, including authentication, authorization, injection, SSRF, path traversal, secrets, unsafe deserialization, data exposure, and insecure failure behavior.

### How `security-review` differs

The skill performs an explicit, on-demand threat review. It identifies:

- actors and assets;
- entry points and trust boundaries;
- security assumptions;
- attack preconditions;
- potential impact;
- evidence and recommended remediation;
- verification requirements;
- areas that could not be verified.

It returns `PASS`, `PASS WITH RESERVATIONS`, or `FAIL`. It does not automatically alter the code.

It requires no hook, script, additional model call, service, or language-specific scanner.

### Trade-offs

Anthropic's official plugin is significantly more advanced. It combines immediate pattern warnings, automatic LLM diff review, agentic commit review, multi-file data-flow analysis, and repository-specific security policies.

The lightweight skill cannot provide the same continuous coverage or enforcement. It can miss vulnerabilities and must not be described as a security scanner or guarantee.

### Recommended positioning

Present it as a transparent threat-modeling assistant or manual security gate that complements automated security tooling. A more specific name such as `threat-model-change` would communicate that role more accurately.

## When to use another tool

Use another tool when the project requires:

- automatic review after every edit or commit;
- enforcement through hooks;
- static or dynamic security analysis;
- independent multi-agent review;
- GitHub pull-request comments and metadata;
- code-coverage measurement;
- dependency vulnerability databases;
- formal compliance evidence;
- guaranteed prevention of unsafe modifications.

Agent skills influence model behavior. They are not a hard security boundary and do not replace CI, linters, tests, scanners, access controls, or human approval.

## Suggested future specialization

The clearest long-term differentiation would be:

| Current skill | Possible specialized direction |
|---|---|
| `challenge-change` | Keep as-is; it already has a distinct pre-decision role |
| `review-implementation` | Focus on evidence-backed diff gating and introduced regressions |
| `debug-systematically` | Specialize in production incidents and distributed request flows |
| `explain-architecture` | Specialize in tracing one request or user journey end to end |
| `prepare-pr` | Keep as a non-mutating release-readiness gate |
| `security-review` | Specialize in threat modeling changes that cross trust boundaries |

These specializations reduce overlap with existing public plugins while preserving a coherent collection centered on deliberate, evidence-based engineering decisions.
