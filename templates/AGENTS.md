# AGENTS.md

Repository entry point for agent instructions.

Keep this file short. It routes to domain-specific guidance.

## Instruction precedence

1. Direct user request
2. Nearest `AGENTS.md` in the file tree (domain-specific)
3. Root `AGENTS.md` (this file)
4. Linked docs under `docs/agent/`
5. Existing code patterns in touched files

## Layered model used in this repo

- Root rules: `AGENTS.md`
- Domain rules: nearest `AGENTS.md` inside domain folders
- Temporary/local overrides: `AGENTS.override.md` (optional)

## Repository map

- Client: `{{CLIENT_PATH}}`
- Server: `{{SERVER_PATH}}`
- Shared contracts: `{{SHARED_PATH}}`
- Human-facing docs: `docs/`
- Agent operating docs: `docs/agent/`
- Repo-local skills: `.agents/skills/`

## Source-of-truth docs

- Linear issue tracker is the primary execution source of truth.
- `docs/agent/core-beliefs.md`
- `docs/agent/architecture.md`
- `docs/agent/security.md`
- `docs/agent/quality.md`
- `docs/agent/ai-native-team.md`
- `docs/agent/mcp-setup.md`
- `docs/agent/workflows.md`
- `docs/agent/skills.md`
- `docs/agent/exec-plans/README.md`

## Multi-agent default loop

1. Plan in Linear issue(s) as the primary record
2. Implement with clear file ownership boundaries
3. Review against `docs/agent/security.md` and `docs/agent/quality.md`
4. Validate with lint/tests for changed scope
5. For exceptional high-risk/audit cases only, use `docs/agent/exec-plans/active/` and close in `docs/agent/exec-plans/completed/`

## Documentation policy

- Keep root `AGENTS.md` as a router, not a rule dump.
- Put detailed constraints in the closest domain `AGENTS.md`.
- Keep docs current; stale instruction files are defects.
