# Changelog

All notable changes to this project will be documented in this file.

## [0.3.0] - 2026-02-27
### Added
- Added `templates/docs/agent/harness-efficiency.md` with compact execution-brief, short-loop, and tool-routing guidance.

### Changed
- Updated template `AGENTS.md` with operational guardrails:
  - no `.env*` edits unless explicitly requested
  - no delete-to-fix-lint/type changes without user approval
  - atomic, path-scoped commits and safer git-path quoting guidance
  - non-interactive rebase guidance and explicit no-amend-by-default rule
- Updated agent docs templates to reference harness-efficiency guidance (`docs/README.md`, `docs/agent/README.md`, `docs/agent/workflows.md`, `docs/agent/skills.md`, `docs/agent/mcp-setup.md`, `docs/agent/core-beliefs.md`, `docs/agent/security.md`).
- Updated skill templates to enforce compact execution briefs and looped verification:
  - `linear-plan-phase`
  - `linear-implement-phase`
  - `multi-agent-orchestrator`
  - `linear-review-phase`
  - `linear-mcp-issue-ops`
  - `agent-kit-repo-adjuster`
  - `agent-kit-updater`
- Updated human prompt template (`templates/docs/human/multi-agent-prompts.md`) to describe expected implement-loop behavior.
- Added repository-level GitHub Copilot instructions at `.github/copilot-instructions.md` with explicit code-review guidance for this repo's agent-first template purpose.

## [0.2.2] - 2026-02-23
### Changed
- Added GitHub Copilot CLI-specific orchestration guidance to use `/fleet` for parallel subagents and `/tasks` for task monitoring.
- Added explicit Copilot CLI fallback guidance to execute dependency waves sequentially when fleet mode is unavailable.
- Clarified that only non-conflicting same-wave work should run in parallel, while same-file or dependency-linked work remains sequential.

## [0.2.1] - 2026-02-23
### Changed
- Updated `linear-review-phase` skill to require closing the tracked issue after review passes and required changes are committed.
- Added explicit review output requirement to report closure status (`closed` or `left open`) with rationale.

## [0.2.0] - 2026-02-22
### Added
- Added `agent-kit-updater` skill to provide a deterministic, non-destructive upgrade workflow for already-installed kits.
- Added upgrade prompt guidance to human docs (`templates/docs/human/multi-agent-prompts.md` and `templates/docs/human/README.md`).

### Changed
- Updated README upgrade instructions to explicitly require `agent-kit-updater` and a post-update `agent-kit-repo-adjuster` pass.
- Added `agent-kit-updater` to the agent skills index.

## [0.1.0] - 2026-02-20
### Added
- Initial version tracking for the Kit.
- Added a setup step to configure the base Linear project/team during agent initialization.
- Added update documentation in README for subsequent kit version upgrades, allowing agents to selectively update touched files.
