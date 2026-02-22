# Changelog

All notable changes to this project will be documented in this file.

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
