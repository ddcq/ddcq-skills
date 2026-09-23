# Contributing

## Adding a Skill

1. Create `skills/<skill-name>/SKILL.md` with frontmatter:

   ```yaml
   ---
   name: <skill-name>
   description: <when to use this skill>
   ---
   ```

2. Keep the skill focused: one job, short workflow (max ~6 steps).
3. Register it in `.claude-plugin/plugin.json` under `skills`.

## Skill Guidelines

- One responsibility per skill.
- `description` must state trigger conditions ("Use when...").
- Body: numbered workflow, then rules. Concise.
- No fluff, no filler. Fragments OK.

## Commits

- Conventional Commits (`feat:`, `fix:`, `docs:`, ...).
- Subject ≤ 50 chars.

## Release

- Update `CHANGELOG.md` under `[Unreleased]`.
- Bump `version` in `.claude-plugin/plugin.json` and `marketplace.json`.
