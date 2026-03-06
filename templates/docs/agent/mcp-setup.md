# MCP Setup Notes

Document repo-specific MCP requirements here.

## Recommended sections

- Required MCP servers/tools
- Authentication prerequisites
- Known limitations
- Validation checks to confirm setup
- Daemonized runner prerequisites when `WORKFLOW.md` is used:
  - `LINEAR_API_KEY` is available to the runner environment
  - the coding-agent runtime referenced by `codex.command` is installed
  - `workspace.root` points to a writable operator-owned path outside the repository checkout
- Tool selection order:
  - local deterministic repo tools first (`rg`, lint/tests, repo scripts)
  - MCP tools for system-of-record operations
  - web/browser research only for external or time-sensitive knowledge gaps
- Missing MCP fallback: if Linear MCP is unavailable, stop issue-driven flow and provide https://linear.app/docs/mcp
