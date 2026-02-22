# Multi-Agent Workflows

## Collaboration pattern

1. Manager defines scope and ownership boundaries.
2. Planner creates/updates issue context (when using issue-driven execution).
3. Implementers execute disjoint scopes.
4. Reviewer checks `security.md` and `quality.md`.
5. Verifier runs checks and reports evidence.
6. Manager closes with outcomes and follow-ups.

## Planner-first issue intake

This enables prompts like: `implement issue DIM-123`.

Linear issues are the default source of truth for plan/execution state.
Planner should label the main issue as `issue-role:top-level` so it is easy to filter in Linear views.
Use `docs/agent/exec-plans/` only for exceptional high-risk/audit-heavy work.

## Handoff template

```md
Task: <title>
Objective: <desired outcome>

Scope in:

- <paths>

Scope out:

- <paths>

Constraints:

- Preserve security and access-control behavior.
- Keep contract compatibility unless explicitly requested.

Checks:

- Lint/tests for changed scope
- Reviewer pass against docs/agent/security.md and docs/agent/quality.md
- Verification evidence (commands + pass/fail)
```
