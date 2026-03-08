# Multi-Agent Workflows

Default efficiency rules: `docs/agent/harness-efficiency.md`

Optional runtime contract: `WORKFLOW.md`

## Collaboration pattern

1. Manager defines scope and ownership boundaries.
2. Planner creates/updates issue context (when using issue-driven execution).
3. Implementers execute disjoint scopes.
4. Reviewer checks `security.md` and `quality.md`.
5. Verifier runs checks and reports evidence.
6. Manager updates `.agents/latest-work.md` with done work and next steps.
7. Manager updates `.agents/system-context.md` when stable downstream context changed.
8. Manager closes with outcomes and follow-ups.

## Efficiency constraints

1. Start each implementation wave with a compact execution brief.
2. Keep patches small and ownership-disjoint before parallelizing.
3. Run verification in each wave, not only at final merge.
4. Give each wave or subagent a fresh context pack instead of accumulated chat history.
5. Use orchestration only when issue structure or risk level requires it.

## Memory model

- Linear issue(s) remain the planning and execution source of truth.
- `.agents/latest-work.md` stores tactical handoff state.
- `.agents/system-context.md` stores durable implementation memory:
  - shipped capabilities
  - reusable contracts/interfaces
  - established patterns
  - open seams relevant to future work
- `docs/agent/context-memory.md` defines when and how to refresh context from these files.

## Planner-first issue intake

This enables prompts like: `implement issue DIM-123` or `linear-implement next`.

Linear issues are the default source of truth for plan/execution state.
When `WORKFLOW.md` exists, keep its tracker states, concurrency, and workflow guardrails aligned with these docs.
Do not treat `WORKFLOW.md` as a substitute for repo-specific instruction files; it is the runtime contract layered under them.
Planner should label the main issue as `issue-role:top-level` so it is easy to filter in Linear views.
Use `docs/agent/exec-plans/` only for exceptional high-risk/audit-heavy work.
For dependency-linked issues, planner should record compact `Consumes`, `Produces`, and `Preserve` contracts in the issue body or execution brief.

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
