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
2. Define in-scope and out-of-scope boundaries.
3. Identify constraints and invariants from `docs/agent/security.md` and `docs/agent/quality.md`.
4. Define acceptance checks.
5. Decompose by ownership (client/server/shared/reviewer/verifier).
6. Choose ticket strategy:
   - small/bounded: create one implementation issue
   - medium/large or dependency-heavy: create orchestration parent issue plus child implementation/review/verification issues
7. Set execution routing label on the main issue:
   - `execution-mode:single` for direct execution
   - `execution-mode:orchestrated` for parent-child orchestration
8. Set deterministic decision labels on the main issue:
   - `risk:low` | `risk:medium` | `risk:high`
   - `scope:client` | `scope:server` | `scope:shared` | `scope:fullstack`
   - `verification:standard` | `verification:strict`
9. Add `done-when` checklist in the main issue body (3-6 concrete acceptance bullets).
10. Create or update issue(s) with objective, scope, checklist, and dependencies.
11. Only for exceptional high-risk/audit work, also create a companion exec-plan file under `docs/agent/exec-plans/active/`.

## Output contract

Always return:
- issue references (`{{ISSUE_PREFIX}}-123` and URL)
- main issue ID for execution
- execution routing label set on main issue (`execution-mode:single` or `execution-mode:orchestrated`)
- decision labels set on main issue (`risk:*`, `scope:*`, `verification:*`)
- `done-when` checklist added to main issue body
- selected ticket strategy (single issue vs orchestration parent + children)
- concise scope summary
- execution checklist for implementer
- explicit blockers/open questions
- next command hint for user: `linear-implement <MAIN-ISSUE-ID>`
