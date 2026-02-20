# Quality Gate

## Required before completion

- Lint/tests for changed scope are run and reported.
- Behavior changes include matching docs updates.
- Residual risks and follow-ups are explicitly listed.

## Change quality rules

- Keep diffs bounded to in-scope files.
- Preserve compatibility unless the task explicitly changes contracts.
- Prefer deterministic behavior over implicit side effects.
