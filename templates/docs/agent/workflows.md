# Multi-Agent Workflows

Default efficiency rules: `docs/agent/harness-efficiency.md`

## Collaboration pattern

1. Manager defines scope and ownership boundaries.
2. Planner creates/updates issue context (when using issue-driven execution).
3. Implementers execute disjoint scopes.
4. Reviewer checks `security.md` and `quality.md`.
5. Verifier runs checks and reports evidence.
6. Manager closes with outcomes and follow-ups.

## Efficiency constraints

1. Start each implementation wave with a compact execution brief.
2. Keep patches small and ownership-disjoint before parallelizing.
3. Run verification in each wave, not only at final merge.
4. Use orchestration only when issue structure or risk level requires it.

## Planner-first issue intake

This enables prompts like: `implement issue DIM-123`.

Linear issues are the default source of truth for plan/execution state.
Planner should label the main issue as `issue-role:top-level` so it is easy to filter in Linear views.
Use `docs/agent/exec-plans/` only for exceptional high-risk/audit-heavy work.

## GitHub Copilot CLI runtime note

When this workflow is executed in GitHub Copilot CLI:

- enable `/fleet` for orchestrated parallel subagent runs,
- use `/tasks` to monitor/wait for active subagents,
- parallelize only non-conflicting tasks in the same dependency wave,
- keep same-file and dependency-linked tasks sequential,
- fallback to sequential wave execution if `/fleet` is disabled or unavailable.

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
