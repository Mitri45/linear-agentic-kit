# Security Invariants

## Data and access safety

- Preserve access-control behavior and authorization boundaries.
- Validate ownership and cross-entity references before writes.
- Keep sensitive operations explicit and auditable.

## API safety

- Validate external inputs.
- Use centralized error handling patterns where available.
- Avoid introducing behavior that bypasses existing auth middleware.
