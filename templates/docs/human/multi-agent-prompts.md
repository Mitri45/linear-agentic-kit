# Multi-Agent Prompt Patterns

Use short prompts. The agent should ask clarification questions when needed.

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

## Implement from issue

```md
linear-implement <ISSUE-ID>
```

Expected behavior:
- agent writes a compact execution brief before code changes
- agent runs short propose -> implement -> verify loops
- agent reports verification evidence and residual risks

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
