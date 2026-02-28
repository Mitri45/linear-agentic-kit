---
name: remind-me
description: Use this skill when the user asks "remind me" to get the latest done work and immediate next steps in this repository.
version: 1.0.0
---

# Remind Me

Use this skill for fast session re-entry and context recall.

## Trigger intent

- `remind me`
- `what was done here`
- `what is next in this repo`

## Required workflow

1. Read `.agents/latest-work.md`.
2. If the file does not exist, create it from `templates/.agents/latest-work.md` shape and bootstrap minimal values from git history/status.
3. Extract and report:
   - latest completed item(s)
   - files touched
   - verification evidence
   - next steps
   - blockers/risks
4. If working tree changed after the snapshot timestamp, mention the delta (`git status --short` summary) before returning next steps.
5. Keep response compact and action-first.

## Output contract

Always return:
- snapshot timestamp
- latest done summary
- next 1-3 concrete steps
- blockers/risks (or explicit none)
