# Harness Efficiency Guide

This guide turns short prompts into deterministic team behavior.

## Core rules

1. Start with a short execution brief before coding:
   - objective
   - in-scope and out-of-scope
   - constraints/invariants
   - expected checks
2. Keep prompts outcome-oriented and repository-specific.
3. Run in short loops:
   - propose
   - implement
   - verify
   - summarize residual risk
4. Keep blast radius small:
   - one owner per file set
   - one concern per patch when possible
   - parallelize only disjoint scopes
5. Verify in the same loop as implementation.
6. Escalate to orchestration only when issue graph or ownership boundaries require it.

## Tool routing policy

1. Prefer local deterministic tools first (`rg`, repo scripts, tests).
2. Use MCP tools when system-of-record access is needed.
3. Use web/browser research only for external or time-sensitive knowledge.

## Manager handoff contract

Use this structure in issue comments or handoffs:

```md
Objective:
Scope in:
Scope out:
Owner paths:
Risks to watch:
Checks:
Definition of done:
```

## Prompting pattern

Use this compact pattern for implementation sessions:

```md
Goal: <outcome>
Constraints: <must preserve>
Context: <file paths and invariants>
Plan: <2-5 steps>
Execute: apply smallest safe patch set
Verify: run required checks
Report: changed files, evidence, residual risks
```
