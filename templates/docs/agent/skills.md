# Skills Index

## Core orchestration skills installed by agent-kit

- `linear-plan`
- `linear-implement`
- `linear-review-phase`
- `linear-mcp-issue-ops`
- `agent-kit-repo-adjuster`
- `agent-kit-updater`
- `remind-me`

## Internal helper skills

- `multi-agent-orchestrator` (invoked by agent logic when `linear-implement` detects parent/child orchestration mode)

## Operating reference

- `docs/agent/harness-efficiency.md` defines default prompt/loop/tooling behavior used by all skills.
- `WORKFLOW.md` defines the optional repo-owned runtime contract for daemonized issue execution.
- `.agents/latest-work.md` stores latest done/next-step handoff state for "remind me" flows.
- `.agents/system-context.md` stores durable implementation memory for downstream issue execution.

## Post-install requirement

Run `agent-kit-repo-adjuster` once after installation to tailor these docs and skills to this repository.

## Post-update requirement

Run `agent-kit-updater` for version upgrades, then run `agent-kit-repo-adjuster` to re-sync repo-specific tailoring.
