# Copilot Instructions For This Repository

This repository is an agent-first template/source repo, not an end-user application.

## Repository purpose

- Primary artifact: reusable markdown templates under `templates/` for agent behavior.
- Audience: downstream coding agents and maintainers operating kit versions.
- Priority: deterministic, machine-consumable guidance over prose for humans.

## Code review instructions

When reviewing PRs in this repository:

1. Treat changes as framework/template changes that will affect many downstream repos.
2. Prefer consistency, backwards compatibility, and non-destructive upgrade behavior.
3. Verify template integrity:
   - placeholder patterns remain valid where intended (for example `{{CLIENT_PATH}}`)
   - no stale references to removed files/skills
   - instructions remain internally consistent across `AGENTS.md`, `docs/agent/**`, and `.agents/skills/**`
4. Verify release hygiene for template-affecting changes:
   - `VERSION` updated when appropriate
   - `CHANGELOG.md` documents user-visible template behavior changes
5. Flag suggestions that optimize for app-runtime code patterns; this repo is mostly policy/templates, not product runtime code.
6. Enforce safety and governance defaults in reviews:
   - no implicit `.env*` modifications
   - no delete-to-fix-lint guidance without explicit approval
   - no implicit commit amend workflows

## Authoring preferences

- Keep instructions concise, explicit, and testable.
- Avoid vague motivational language; prefer concrete behavioral contracts.
- Preserve existing template structure unless change is necessary and documented.
