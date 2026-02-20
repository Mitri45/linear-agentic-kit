# Linear Agentic Kit

Reference repository for agent operating standards and reusable templates.

This repo is intentionally markdown-first. It is designed to be read by agents and then applied to a target repository.

## User experience target

Humans should be able to run this pattern with short prompts:

- `linear-plan <feature I want to plan>`
- `linear-implement <ISSUE-ID>`
- `linear-review <ISSUE-ID>`

The agent is expected to ask clarification questions when needed, instead of requiring humans to provide long structured briefs.

`linear-implement` is the unified execution entrypoint. The agent chooses direct execution or orchestration mode based on ticket structure.

## How to use this kit in another repo

Give your agent this instruction:

```md
Read https://github.com/Mitri45/linear-agentic-kit/blob/main/README.md and apply Linear Agentic Kit to this repository.
```

Then the agent should execute this workflow:

1. Check that Linear MCP tools are available in the current agent session before applying issue-driven workflows.
2. Ask the user which Linear project/team to use as a base for issue tracking and make sure to configure it.
3. Merge `templates/AGENTS.md` into target repo root `AGENTS.md` non-destructively.
4. Merge `templates/docs/agent/**` into target repo as `docs/agent/**` non-destructively.
5. Merge `templates/docs/human/**` into target repo as `docs/human/**` non-destructively.
6. Merge `templates/docs/README.md` into target repo as `docs/README.md` non-destructively.
7. Merge `templates/.agents/skills/**` into target repo as `.agents/skills/**` non-destructively.
8. Never replace existing instruction files wholesale when they already exist; append or edit-in-place while preserving existing repo rules.
9. Run skill `agent-kit-repo-adjuster` in the target repo.
10. Confirm no placeholder values remain (for example `<set-client-path>`).
11. Explain to the human operator how to run this pattern in day-to-day work (plan, execute, review, verify, close), using `docs/human/*`.
12. Note the installed version from the `VERSION` file so that it can be tracked for future updates.

## Updating an existing installation

To apply a new version of Linear Agentic Kit to an already installed repository:

1. Check the `CHANGELOG.md` in the new kit against the version currently installed in the target repository.
2. Review the `CHANGELOG.md` to determine which specific files were introduced or modified since the installed version.
3. Apply updates to **only the touched files** inside the `.agents`, `docs`, and root instructions in the target repository, merging changes non-destructively to preserve local modifications.
4. Update the stored version in the target repository to match the new kit version.

## Required post-install step

Run this prompt in the target repo:

```md
Use skill agent-kit-repo-adjuster to tailor docs/agent and skills to this repository.
```

## Repository layout

- `templates/AGENTS.md`: root instruction router template
- `templates/docs/agent/`: core operating docs
- `templates/docs/human/`: human-facing runbook and prompt patterns
- `templates/docs/README.md`: docs routing map for humans and agents
- `templates/.agents/skills/`: reusable orchestration skills

## Operating rules for agents applying this kit

1. Do not erase target-repo-specific constraints.
2. If Linear MCP is missing, stop issue-driven setup, report the gap explicitly, and point the user to install docs: https://linear.app/docs/mcp.
3. Keep root `AGENTS.md` concise and routing-focused.
4. Apply non-destructive updates: append/merge preferred, full replace only when file is absent.
5. Update architecture/security/quality docs to reflect actual repository reality.
6. Ensure skill examples and issue references match target issue-key conventions.
7. Prioritize short prompt UX and ask clarification questions proactively when inputs are ambiguous.
8. Report residual gaps explicitly if full adaptation cannot be completed.
