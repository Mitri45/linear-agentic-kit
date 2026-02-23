# Changelog

All notable changes to this project will be documented in this file.

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
