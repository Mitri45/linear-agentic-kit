---
name: linear-implement
description: Use this skill when implementing from issue context with manager-led orchestration.
version: 1.1.0
---

# Issue Implementation Phase

Use this skill for implementation sessions driven by existing issue context.

## Trigger intent (single execution entrypoint)

- `linear-implement <ISSUE-ID>`
- `linear-implement next`

The agent decides execution mode using issue label first, then structure fallback:
- label `execution-mode:single`: execute directly
- label `execution-mode:orchestrated`: orchestrate in waves and parallelize by ownership where safe
- if label missing: infer from issue structure
- single issue: execute directly
- parent issue with dependencies/children: orchestrate in waves and parallelize by ownership where safe

### Next ticket selection logic (`linear-implement next`)

When `linear-implement next` is invoked, the agent must:
1. Query Linear for issues assigned to `me` in an active development state (e.g., `In Progress`, `Ready for Dev`, `To Do`).
2. Identify the "next" candidate by applying these filters and sorts in order:
   - **Unblocked:** Exclude issues with active `blockedBy` relations.
   - **Priority:** Sort by priority (1=Urgent, 2=High, 3=Normal, 4=Low, 0=None).
   - **Order:** Use Linear `sortOrder` if available.
   - **Context:** Check `.agents/latest-work.md` for a previously identified "next step".
3. Validate the selected issue:
   - Ensure it has enough context (description, checklist/acceptance criteria).
   - If context is missing, suggest running `linear-plan <ISSUE-ID>` first.
4. Proceed with implementation of the validated issue.

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
2. Read `.agents/system-context.md` and `.agents/latest-work.md` before coding.
3. Derive objective/scope/checklist from issue content and write a compact execution brief.
4. Build a fresh context pack for the issue:
   - objective and `done-when`
   - `Consumes` / `Produces` / `Preserve` contracts from the issue when present
   - relevant entries from `.agents/system-context.md`
   - tactical next-step state from `.agents/latest-work.md`
   - only the code paths needed for current scope
5. Apply `docs/agent/harness-efficiency.md` loop: propose -> implement -> verify -> summarize.
6. Resolve execution mode from main issue label `execution-mode:*`; if absent, infer from issue structure.
7. Read decision labels from main issue:
   - `risk:*` determines default caution level
   - `scope:*` determines ownership routing boundaries
   - `verification:*` determines verification depth
   - if `WORKFLOW.md` is installed, follow its runtime contract in addition to `AGENTS.md`
8. Keep implementation bounded to issue scope unless explicitly expanded.
9. Respect safety guardrails from `AGENTS.md` (no `.env*` edits unless requested; no delete-to-fix-lint without approval).
10. Parallelize only disjoint ownership scopes.
11. If the session becomes noisy, crosses a task boundary, or starts leaning on stale chat state, rebuild from the context pack instead of continuing from accumulated conversation history.
12. Use Linear issue(s) as the primary execution record.
13. Only for exceptional high-risk/audit/incident cases, create/update `docs/agent/exec-plans/active/YYYYMMDD-<slug>.md`.
14. Run reviewer pass against `docs/agent/security.md` and `docs/agent/quality.md`.
15. Run verifier checks and capture command evidence according to `verification:*` label.
16. Validate completion against the issue `done-when` checklist.
17. Update issue with outcome notes and verification summary.
18. Update `.agents/latest-work.md` with latest done work, touched files, verification, and next step.
19. Update `.agents/system-context.md` when the completed work changed stable capabilities, contracts, patterns, or seams that later work should inherit.
20. If an exec-plan was used, move it to `docs/agent/exec-plans/completed/`.

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
- confirmation that `.agents/latest-work.md` was updated
- confirmation that `.agents/system-context.md` was updated or explicitly left unchanged
- next command hint for user where relevant (for example `linear-review <ISSUE-ID>`)
