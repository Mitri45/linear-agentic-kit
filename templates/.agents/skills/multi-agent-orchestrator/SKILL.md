---
name: multi-agent-orchestrator
description: Use this skill to run manager-led multi-agent execution with plan gating, file ownership boundaries, reviewer/verifier checks, and plan closure.
version: 1.0.0
---

# Multi-Agent Orchestrator

Use this skill when a task should run with a manager + specialist workflow instead of a single-agent change.

## Trigger intent

- `multi-agent-orchestrator <ISSUE-ID>`
- `orchestrate <ISSUE-ID>`
- `execute parent issue <ISSUE-ID>`

If the input is an issue ID (for example `DIM-14`), treat it as the root orchestration issue.

## Default operating contract

1. Follow nearest `AGENTS.md` and `docs/agent/*`.
2. Start with the manager handoff contract from `docs/agent/harness-efficiency.md`.
3. If input is a root issue:
   - load parent issue details
   - discover child issues
   - load dependency edges (`blockedBy` / `blocks`)
   - build dependency waves (topological order)
   - execute same-wave issues in parallel when ownership is disjoint
   - gate each wave on reviewer/verifier checks
   - when running in GitHub Copilot CLI:
     - enable `/fleet` for same-wave parallel subagents
     - use `/tasks` to track and wait for subagent completion
     - if `/fleet` is unavailable, execute the same waves sequentially
4. Use Linear parent/child issues as the primary orchestration record.
5. Only for exceptional high-risk/audit/incident cases, create a plan in `docs/agent/exec-plans/active/YYYYMMDD-<slug>.md`.
6. Decompose by file ownership:
   - client: `{{CLIENT_PATH}}`
   - server: `{{SERVER_PATH}}`
   - shared: `{{SHARED_PATH}}`
7. Assign mode per task: `delegate`, `review`, or `own`.
8. Run reviewer pass against:
   - `docs/agent/security.md`
   - `docs/agent/quality.md`
9. Run verifier checks and capture command evidence.
10. If formal plan was used, move plan to `docs/agent/exec-plans/completed/`.
