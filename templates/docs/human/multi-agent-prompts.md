# Multi-Agent Prompt Patterns

Use short prompts. The agent should ask clarification questions when needed.

If the repo uses a daemonized issue runner, keep `WORKFLOW.md` in sync with `AGENTS.md` and `docs/agent/*`.

## Session reminder

```md
remind me
```

Expected behavior:
- agent reads `.agents/latest-work.md`
- agent reads `.agents/system-context.md` when present
- agent summarizes latest completed work and verification
- agent lists the next concrete steps

## Plan a feature

```md
linear-plan <feature I want to plan>
```

Expected behavior:
- agent asks clarification questions first when scope is ambiguous
- agent returns a concrete plan and issue-ready breakdown
- agent sets decision labels on main issue:
  - `execution-mode:*`, `risk:*`, `scope:*`, `verification:*`
- agent sets hierarchy label on main issue:
  - `issue-role:top-level` (required so top-level work can be filtered in Linear views)
- agent adds `done-when` checklist to main issue body
- agent records `Consumes` / `Produces` / `Preserve` contracts when work depends on upstream slices or establishes downstream contracts

## Implement from issue

```md
linear-implement <ISSUE-ID>
linear-implement next
```

Expected behavior:
- agent writes a compact execution brief before code changes
- agent rebuilds a fresh context pack from issue context, `.agents/system-context.md`, and `.agents/latest-work.md`
- agent runs short propose -> implement -> verify loops
- agent reports verification evidence and residual risks
- agent updates `.agents/latest-work.md` with latest done + next steps
- agent updates `.agents/system-context.md` when stable capabilities, contracts, or patterns changed
- agent follows `WORKFLOW.md` when that file is installed
- for `linear-implement next`, agent selects and validates the next ticket based on assignment, status, priority, and dependencies.

## Review from issue

```md
linear-review <ISSUE-ID>
```

Execution note:
- `linear-implement <ISSUE-ID>` is always the entrypoint.
- agent uses issue label first for routing:
  - `execution-mode:single`
  - `execution-mode:orchestrated`
- if label is missing, agent falls back to issue-structure detection.

## Repo adaptation after kit install

```md
Use skill agent-kit-repo-adjuster to tailor docs/agent and skills to this repository.
Then explain to me how to operate this workflow as a human.
```

## Upgrade an existing kit install

```md
Use skill agent-kit-updater to upgrade this repository's local kit to the new version non-destructively.
Then run agent-kit-repo-adjuster and summarize what changed.
```
