---
name: agent-kit-repo-adjuster
description: Run immediately after template copy to tailor the installed kit to this repository's actual structure, security model, and workflows.
version: 1.0.0
---

# Agent Kit Repo Adjuster

Use this skill once right after copying kit templates into a repository.

## Goal

Convert generic kit defaults into repo-accurate guidance.

## Required workflow

1. Inspect repository structure and identify real ownership boundaries.
2. Update these files with concrete paths and technology details:
   - `AGENTS.md`
   - `docs/agent/architecture.md`
   - `docs/agent/security.md`
   - `docs/agent/quality.md`
   - `docs/agent/harness-efficiency.md`
   - `docs/agent/workflows.md`
3. Update orchestration skills to align examples and constraints:
   - `.agents/skills/multi-agent-orchestrator/SKILL.md`
   - `.agents/skills/linear-plan-phase/SKILL.md`
   - `.agents/skills/linear-implement-phase/SKILL.md`
   - `.agents/skills/linear-review-phase/SKILL.md`
4. Add domain-level `AGENTS.md` files where needed (for example under major app folders).
5. Validate that required files exist and placeholders are fully resolved.

## Minimum acceptance criteria

- No placeholder paths remain (e.g. `<set-client-path>`).
- Architecture/security docs reflect actual code layout and invariants.
- Workflow docs contain repo-appropriate lint/test commands using `{{PACKAGE_MANAGER}}`.
- Harness efficiency docs and references are present and aligned across skills/workflows.
- Skill examples use the repo's issue key style (for example `DIM-123`).

## Output contract

Always return:
- files updated
- key repo-specific constraints captured
- verification command output summary
- residual gaps to refine later
