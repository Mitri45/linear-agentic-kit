---
name: agent-kit-updater
description: Use this skill when updating an already-installed Linear Agentic Kit in a repository to a newer kit version.
version: 1.0.0
---

# Agent Kit Updater

Use this skill when a repository already has Linear Agentic Kit installed and needs a version upgrade.

## Trigger intent

- `run agent-kit-updater`
- `upgrade linear-agentic-kit to <VERSION>`
- `update local kit from <OLD_VERSION> to <NEW_VERSION>`
- `apply latest linear-agentic-kit updates`

Minimal trigger support:
- If user says only `run agent-kit-updater`, treat it as:
  - upgrade this repo to the latest kit version available in the source kit
  - auto-detect current version from target repo `VERSION`
  - run post-update `agent-kit-repo-adjuster`
  - return changed files and merge notes

## Required workflow

1. Detect currently installed kit version from the target repo `VERSION` file.
2. Determine target version:
   - if user provided version, use it
   - otherwise use latest available source kit version
3. Compare installed version with the source kit version being applied.
4. Read source `CHANGELOG.md` and identify files touched since installed version.
5. Update only touched kit-managed files:
   - root instructions (`AGENTS.md`)
   - `docs/**`
   - `.agents/skills/**`
   - `VERSION`
6. Merge non-destructively. Preserve existing repo-specific constraints and local customizations.
7. Do not replace whole files when targeted edits or append/merge can preserve local guidance.
8. If touched files include templates with placeholders, resolve placeholders to repo-accurate values.
9. Run `agent-kit-repo-adjuster` after structural updates to ensure docs/skills remain repo-accurate.
10. Verify no unresolved placeholders remain and no stale skill references exist.
11. Verify `docs/agent/harness-efficiency.md` exists and is referenced by workflow/skills docs when present in source version.
12. Summarize what changed, what was intentionally left unchanged, and any manual follow-ups.

## Minimum acceptance criteria

- Installed `VERSION` in target repo matches the applied kit version.
- All changes map to entries in source `CHANGELOG.md` since prior version.
- No repo-specific constraints were removed.
- `docs/agent/skills.md` matches actual installed skills.

## Output contract

Always return:
- previous installed version and new installed version
- list of files updated
- non-destructive merge notes for files with local customizations
- verification summary (placeholder check + basic sanity checks)
- residual follow-ups (if any)
