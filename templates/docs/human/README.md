# Human Operator Guide

This guide explains how to run the multi-agent orchestration pattern day to day.

## Standard loop

1. Use Linear issue(s) as the main planning and execution record.
2. Ask agent to execute with explicit scope and ownership boundaries.
3. Require review against `docs/agent/security.md` and `docs/agent/quality.md`.
4. Require verification evidence (commands + pass/fail).
5. For exceptional high-risk/audit work only, maintain an exec-plan in `docs/agent/exec-plans/` and move it to `completed/` at closure.
6. Require agent to update `.agents/latest-work.md` so a new session can start with `remind me`.
7. Require agent to update `.agents/system-context.md` whenever completed work changes stable capabilities, contracts, or patterns.
8. If the repo uses a daemonized issue runner, require `WORKFLOW.md` to stay aligned with repo rules and issue states.

## Issue-driven mode (Linear MCP)

- Use issue context as system of record for medium/large tasks.
- Ensure agent confirms Linear MCP availability before issue-driven execution.
- If Linear MCP is not found, require the agent to provide install instructions URL: https://linear.app/docs/mcp.
- Ask agent to post outcome notes and verification summary back to issue.

## Daemonized runner mode (`WORKFLOW.md`)

- Use this only when the repository wants unattended or scheduled issue pickup.
- Require the agent to confirm placeholders are resolved and Linear state names are accurate before enabling the runner.
- Keep workspace roots outside the repository checkout and in an operator-owned writable path.
- Start with conservative concurrency and increase it only after real runs prove safe ownership boundaries and cleanup behavior.

## Updating kit version in an existing repo

- Ask agent to run `agent-kit-updater` when upgrading the repository to a newer kit version.
- Require non-destructive merges so repo-specific instructions remain intact.
- Require a post-update `agent-kit-repo-adjuster` pass.
- If `WORKFLOW.md` is installed, require placeholder resolution and state/concurrency review after the upgrade.

## Recommended issue labels for predictable decisions

- `execution-mode:single` | `execution-mode:orchestrated`
- `risk:low` | `risk:medium` | `risk:high`
- `scope:client` | `scope:server` | `scope:shared` | `scope:fullstack`
- `verification:standard` | `verification:strict`
- `issue-role:top-level` on the main issue (required for Linear list/view filtering)

Also keep a `done-when` checklist in the main issue body (3-6 concrete bullets).

## Verification levels

- `verification:standard`:
  - changed-scope lint/type-check/tests
  - command evidence with pass/fail
  - completion mapped to `done-when`
- `verification:strict`:
  - all standard checks
  - integration/e2e/parity checks when applicable
  - explicit evidence for each `done-when` bullet

## Operator checklist per task

- Objective and scope are explicit.
- In-scope and out-of-scope paths are listed.
- Upstream `Consumes` and downstream `Produces` contracts are explicit when work is dependency-linked.
- Required checks are listed.
- Risks/follow-ups are documented before closure.
