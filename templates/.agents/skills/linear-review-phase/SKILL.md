---
name: linear-review-phase
description: Use this skill when review-only output is needed from issue context.
version: 1.1.0
---

# Issue Review Phase

Use this skill for review-only sessions driven by issue context.

## Required workflow

1. Resolve and read the target issue.
2. Gather review scope from objective/scope/checklist.
3. Apply adversarial checks for changed scope:
   - correctness/regressions
   - security/access-control risks
   - compatibility risks
   - missing tests/verification gaps
4. Validate critical claims with evidence.
5. Confirm implementer followed `docs/agent/harness-efficiency.md` loop and reported residual risks.
6. Update issue with findings and verification summary.
7. If review is passed and required changes are committed, close the issue.
   - confirm acceptance state is explicit (approved/no findings or findings resolved)
   - confirm commit reference(s) are recorded on the issue
   - set issue to a closed/done state in the tracker
8. Update `.agents/latest-work.md` with review outcome and follow-up actions.

## Output contract

Always return:
- issue reference used (`DIM-123` and URL)
- findings ordered by severity (or explicit no-findings)
- verification evidence summary
- closure status (`closed` or `left open`) with reason
- residual risks/follow-ups
- confirmation that `.agents/latest-work.md` was updated
