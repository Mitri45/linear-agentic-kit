---
name: linear-plan
description: Use this skill when planning-only execution is requested and issue context should be created or updated without coding.
version: 1.0.0
---

# Issue Planning Phase

Use this skill for planner-only sessions.

## Trigger intent (simple UX)

- `linear-plan <feature request>`
- `linear-plan <problem statement>`

If the request is ambiguous, ask clarification questions first, then continue planning.

## Required workflow

1. Ask targeted clarification questions until objective and definition of done are clear.
2. Write a compact execution brief first (objective, scope in/out, constraints, checks).
3. Define in-scope and out-of-scope boundaries.
4. Identify constraints and invariants from `docs/agent/security.md`, `docs/agent/quality.md`, and `docs/agent/harness-efficiency.md`.
5. Define acceptance checks.
6. Decompose by ownership (client/server/shared/reviewer/verifier).
7. Choose ticket strategy:
   - small/bounded: create one implementation issue
   - medium/large or dependency-heavy: create orchestration parent issue plus child implementation/review/verification issues
8. Set execution routing label on the main issue:
   - `execution-mode:single` for direct execution
   - `execution-mode:orchestrated` for parent-child orchestration
9. Set deterministic decision labels on the main issue:
   - `risk:low` | `risk:medium` | `risk:high`
   - `scope:client` | `scope:server` | `scope:shared` | `scope:fullstack`
   - `verification:standard` | `verification:strict`
10. Set issue hierarchy label on the main issue:
   - `issue-role:top-level` (required for Linear view filtering)
11. Add `done-when` checklist in the main issue body (3-6 concrete acceptance bullets).
12. Create or update issue(s) with objective, scope, checklist, and dependencies.
13. Only for exceptional high-risk/audit work, also create a companion exec-plan file under `docs/agent/exec-plans/active/`.
14. Update `.agents/latest-work.md` with planning outcomes and next execution step.

## Output contract

Always return:
- issue references (`DIM-123` and URL)
- main issue ID for execution
- execution routing label set on main issue (`execution-mode:single` or `execution-mode:orchestrated`)
- decision labels set on main issue (`risk:*`, `scope:*`, `verification:*`)
- issue hierarchy label set on main issue (`issue-role:top-level`)
- `done-when` checklist added to main issue body
- selected ticket strategy (single issue vs orchestration parent + children)
- concise scope summary
- execution checklist for implementer
- explicit blockers/open questions
- confirmation that `.agents/latest-work.md` was updated
- next command hint for user: `linear-implement <MAIN-ISSUE-ID>`
