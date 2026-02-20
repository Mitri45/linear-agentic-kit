# Human Operator Guide

This guide explains how to run the multi-agent orchestration pattern day to day.

## Standard loop

1. Use Linear issue(s) as the main planning and execution record.
2. Ask agent to execute with explicit scope and ownership boundaries.
3. Require review against `docs/agent/security.md` and `docs/agent/quality.md`.
4. Require verification evidence (commands + pass/fail).
5. For exceptional high-risk/audit work only, maintain an exec-plan in `docs/agent/exec-plans/` and move it to `completed/` at closure.

## Issue-driven mode (Linear MCP)

- Use issue context as system of record for medium/large tasks.
- Ensure agent confirms Linear MCP availability before issue-driven execution.
- Ask agent to post outcome notes and verification summary back to issue.

## Recommended issue labels for predictable decisions

- `execution-mode:single` | `execution-mode:orchestrated`
- `risk:low` | `risk:medium` | `risk:high`
- `scope:client` | `scope:server` | `scope:shared` | `scope:fullstack`
- `verification:standard` | `verification:strict`

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
- Required checks are listed.
- Risks/follow-ups are documented before closure.
