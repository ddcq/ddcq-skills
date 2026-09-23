---
name: explain-architecture
description: Explain an unfamiliar repository, feature, module, or request flow using evidence from the codebase. Use when a user asks how code works, where behavior is implemented, or what components and dependencies are involved.
---

# Explain Architecture

Start from the user-visible behavior or entry point. Inspect project instructions, routes or commands, primary modules, callers, dependencies, data models, external boundaries, tests, and configuration. Follow the real execution path rather than inferring architecture from filenames.

Explain:

1. entry point and trigger;
2. main components and responsibilities;
3. data and control flow;
4. external systems and failure boundaries;
5. important invariants and project conventions;
6. tests and observability;
7. likely extension points and risks.

Use paths and symbols as evidence. Distinguish verified behavior from inference. Prefer a compact flow diagram or table when it clarifies relationships. End with unanswered questions and the smallest set of files to read next.
