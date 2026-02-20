---
name: linear-mcp-issue-ops
description: Use issue tracker MCP as the system of record after plan approval.
version: 1.0.0
---

# Issue Ops

Use this skill for planning handoff, issue creation, and issue-driven execution.

## Required behavior

1. No implementation starts before issue context is read.
2. Every medium/large task maps to at least one issue.
3. Issue links are recorded in `docs/agent/exec-plans/active/<plan>.md`.
