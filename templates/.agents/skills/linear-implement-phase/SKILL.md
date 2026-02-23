---
name: linear-implement
description: Use this skill when implementing from issue context with manager-led orchestration.
version: 1.0.0
---

# Issue Implementation Phase

Use this skill for implementation sessions driven by existing issue context.

## Trigger intent (single execution entrypoint)

- `linear-implement <ISSUE-ID>`

This is the only user-facing implementation command.
The agent decides execution mode using issue label first, then structure fallback:
- label `execution-mode:single`: execute directly
- label `execution-mode:orchestrated`: orchestrate in waves and parallelize by ownership where safe
- if label missing: infer from issue structure
- single issue: execute directly
- parent issue with dependencies/children: orchestrate in waves and parallelize by ownership where safe

## GitHub Copilot CLI specific execution rules

Apply this section only when the runtime is GitHub Copilot CLI.

- For orchestrated execution, enable `/fleet` before launching subagents.
- Use `/tasks` to monitor and wait for subagent completion between waves.
- Parallelize only `execution-mode:orchestrated` tasks that are both:
  - in the same dependency wave, and
  - non-conflicting by ownership/file set.
- Keep tasks sequential when they touch the same files, same ownership area, or have dependency edges.
- If `/fleet` is disabled or unavailable, run the same plan sequentially and keep wave gates/review checks unchanged.

## Required workflow

1. Resolve and read the target issue before coding.
2. Derive objective/scope/checklist from issue content.
3. Resolve execution mode from main issue label `execution-mode:*`; if absent, infer from issue structure.
4. Read decision labels from main issue:
   - `risk:*` determines default caution level
   - `scope:*` determines ownership routing boundaries
   - `verification:*` determines verification depth
5. Keep implementation bounded to issue scope unless explicitly expanded.
6. Use Linear issue(s) as the primary execution record.
7. Only for exceptional high-risk/audit/incident cases, create/update `docs/agent/exec-plans/active/YYYYMMDD-<slug>.md`.
8. Run reviewer pass against `docs/agent/security.md` and `docs/agent/quality.md`.
9. Run verifier checks and capture command evidence according to `verification:*` label.
10. Validate completion against the issue `done-when` checklist.
11. Update issue with outcome notes and verification summary.
12. If an exec-plan was used, move it to `docs/agent/exec-plans/completed/`.

## Verification policy (deterministic)

- `verification:standard` minimum:
  - run lint/type-check/tests for changed scope
  - capture command list with pass/fail status
  - map results to `done-when` checklist
- `verification:strict` minimum:
  - all `verification:standard` checks
  - add integration/e2e or parity checks where applicable
  - include negative-path/regression checks for touched risk areas
  - capture explicit evidence for each `done-when` bullet

## Output contract

Always return:
- issue reference used
- changed scope summary
- verification evidence summary
- residual risks/follow-ups
- next command hint for user where relevant (for example `linear-review <ISSUE-ID>`)
