---
name: linear-review-phase
description: Use this skill when review-only output is needed from issue context.
version: 1.0.0
---

# Issue Review Phase

Use this skill for review-only sessions driven by issue context.

## Required workflow

1. Resolve and read the target issue.
2. Gather review scope from objective/scope/checklist.
3. Review for:
   - correctness/regressions
   - security/access-control risks
   - compatibility risks
   - missing tests/verification gaps
4. Validate critical claims with evidence.
5. Update issue with findings and verification summary.

## Output contract

Always return:
- issue reference used (`DIM-123` and URL)
- findings ordered by severity (or explicit no-findings)
- verification evidence summary
- residual risks/follow-ups
