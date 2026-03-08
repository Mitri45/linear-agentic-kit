# Context And Memory

This kit uses two complementary memory artifacts so agents do not rely on stale chat history.

## Memory split

- `.agents/latest-work.md`
  Tactical handoff memory for what just changed, what was verified, and what is next.
- `.agents/system-context.md`
  Durable implementation memory for stable capabilities, interfaces, patterns, and seams that later work should inherit.

## Why this exists

Without file-backed memory, downstream work becomes context-dumb:

- completed capabilities are invisible to later tasks
- agents rediscover the same structure repeatedly
- long conversations accumulate stale tool output and refactor-era assumptions
- execution quality drops as context noise grows

The fix is to keep stable context on disk and rebuild fresh task context from that state.

## Update rules

- Update `.agents/latest-work.md` at the end of every planning, implementation, and review session.
- Update `.agents/system-context.md` whenever completed work changes one of:
  - shipped capability surface
  - reusable contracts/interfaces
  - established implementation patterns
  - known seams or follow-up constraints
- Do not copy transient debugging detail into `.agents/system-context.md`.
- Do not use `.agents/system-context.md` as a roadmap or status board; Linear remains the planning source of truth.

## Context refresh rules

Before implementation, build a compact context pack from:

1. current issue objective and `done-when`
2. `.agents/system-context.md`
3. `.agents/latest-work.md`
4. nearest `AGENTS.md` and `docs/agent/*`
5. only the code paths relevant to the current scope

If the session becomes noisy or crosses a task boundary:

1. stop relying on old conversation state
2. restate the current objective, scope, contracts, patterns, and checks from file-backed memory
3. continue in a fresh subagent or fresh session when available

## Dependency contracts

For dependency-linked work, planners should record a compact contract in the issue body or execution brief:

- `Consumes`: upstream artifacts, interfaces, endpoints, types, or invariants this work assumes
- `Produces`: new artifacts, interfaces, endpoints, types, or invariants downstream work can rely on
- `Preserve`: existing patterns or contracts that must not regress

This gives later slices visibility into what already exists without turning repo docs into a delivery ledger.
