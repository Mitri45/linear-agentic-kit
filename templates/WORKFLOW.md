---
tracker:
  kind: linear
  api_key: $LINEAR_API_KEY
  endpoint: https://api.linear.app/graphql
  project_slug: {{LINEAR_PROJECT_SLUG}}
  active_states:
    # Replace with the repo's actual pre-execution and active development states.
    - Todo
    - In Progress
  terminal_states:
    # Keep this aligned with terminal issue states used in Linear for this repo.
    - Done
    - Cancelled
    - Canceled
    - Duplicate
polling:
  interval_ms: 30000
workspace:
  # Replace with an absolute path owned by the operator environment.
  root: {{WORKSPACE_ROOT}}
hooks:
  timeout_ms: 60000
  before_run: |
    test -f WORKFLOW.md
    test -f AGENTS.md
agent:
  # Keep low by default; raise only after proving ownership boundaries and verification loops.
  max_concurrent_agents: 3
  max_retry_backoff_ms: 300000
codex:
  command: codex app-server
  # Choose approval/sandbox settings for the target runtime explicitly when supported.
  turn_timeout_ms: 3600000
  read_timeout_ms: 5000
  stall_timeout_ms: 300000
---

# Repository Workflow Contract

Use this file as the repo-owned runtime contract for daemonized issue execution.
It is intended for runners such as Symphony or any local orchestrator that polls Linear and launches coding-agent sessions.

## Operator setup

- Resolve all placeholders before enabling the workflow:
  - `{{LINEAR_PROJECT_SLUG}}`
  - `{{WORKSPACE_ROOT}}`
- Keep the workspace root outside the repository checkout to avoid nested worktree confusion.
- Prefer conservative concurrency until the repo has proven ownership boundaries, verification loops, and cleanup behavior.
- Keep tracker states aligned with the actual Linear workflow used by the target repository.

## Required behavior

- Read the target Linear issue and use it as the primary execution record.
- Follow `AGENTS.md`, nearest domain `AGENTS.md`, and `docs/agent/*`.
- Treat `WORKFLOW.md` as runtime configuration, not as a replacement for repo-specific instruction files.
- Treat `.agents/latest-work.md` as session handoff memory.
- Treat `.agents/system-context.md` as durable implementation memory for cross-slice visibility.
- Keep edits inside the issue scope unless the issue explicitly expands scope.
- Respect repo safety rules:
  - no `.env*` edits unless explicitly requested
  - no delete-to-fix-lint/type changes without explicit approval
  - no implicit amend workflows
  - no deploys, destructive operations, or schema/API contract changes without the repo's required approval path

## Execution loop

1. Read the issue and derive a compact execution brief:
   - objective
   - scope in / scope out
   - constraints
   - checks
2. Build a fresh context pack from:
   - issue objective and `done-when`
   - `.agents/system-context.md`
   - `.agents/latest-work.md`
   - nearest `AGENTS.md` and relevant `docs/agent/*`
   - only the code paths needed for the current issue
3. Choose execution mode from issue labels:
   - `execution-mode:single`
   - `execution-mode:orchestrated`
   - if no label exists, infer from issue structure
4. Read decision labels:
   - `risk:*`
   - `scope:*`
   - `verification:*`
   - `issue-role:*`
5. For orchestrated work:
   - parallelize only disjoint ownership/file scopes
   - keep same-file and dependency-linked work sequential
   - give each wave a fresh context pack instead of accumulated conversation history
   - gate each wave on review and verification
6. Run reviewer pass against:
   - `docs/agent/security.md`
   - `docs/agent/quality.md`
7. Run verification according to `verification:*`:
   - `verification:standard`: changed-scope lint/type-check/tests with pass/fail evidence
   - `verification:strict`: add integration/regression evidence mapped to `done-when`
8. Post outcome notes and verification summary back to the issue.
9. Update `.agents/latest-work.md` with latest done work, touched files, verification, and next step.
10. Update `.agents/system-context.md` when stable capabilities, contracts, patterns, or seams changed.
11. Release the workspace only according to the orchestrator's terminal-state cleanup policy; do not delete active workspaces opportunistically.

## Handoff state

A run may stop in a workflow-defined handoff state such as review or human follow-up. Completion does not require auto-closing the issue unless the issue state and verification evidence support closure.
