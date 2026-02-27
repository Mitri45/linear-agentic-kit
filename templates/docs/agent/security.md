# Security Invariants

## Data and access safety

- Preserve access-control behavior and authorization boundaries.
- Validate ownership and cross-entity references before writes.
- Keep sensitive operations explicit and auditable.
- Never modify `.env` or other secret-bearing environment files unless the user explicitly asks.
- Treat deletions as high-risk changes; require explicit user approval when deletion is used only to satisfy lint/type checks.

## API safety

- Validate external inputs.
- Use centralized error handling patterns where available.
- Avoid introducing behavior that bypasses existing auth middleware.
