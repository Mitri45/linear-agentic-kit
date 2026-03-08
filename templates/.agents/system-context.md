# System Context Ledger

This file is the durable implementation memory for the repository.
Update it only with stable information that downstream work should inherit.

Use this alongside `.agents/latest-work.md`:

- `.agents/latest-work.md` = latest session handoff, next step, tactical status
- `.agents/system-context.md` = stable capabilities, contracts, patterns, and seams

## Last refreshed

- timestamp: `<ISO-8601 UTC>`
- branch: `<branch-name>`
- source issue/task: `<ISSUE-ID or short task name>`

## Current shipped capabilities

- `<area>`: `<observable capability now implemented>`

## Contracts and interfaces downstream work depends on

- `<producer area or issue>` -> `<artifact / endpoint / type / command>` -> `<consumer area or issue>`

## Established patterns to preserve

- `<pattern or invariant>`

## Open seams / follow-ups

- `<known limitation, planned extension point, or dependency for later work>`
