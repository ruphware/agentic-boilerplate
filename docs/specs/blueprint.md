# Blueprint — <PROJECT NAME>

Status: Draft | Version: 0.1 | Last Updated: YYYY-MM-DD

## Purpose

Describe the system architecture at a level that makes implementation and change safe.

## Architecture (high-level)

- Components: ...
- Data flow: ...
- Boundaries: ...

## Key Invariants (MUST NOT BREAK)

1) ...
2) ...

## Definition Index (optional, recommended for scale)

If this blueprint grows large, keep it as a stable root and branch into focused sub-specs.

Rules of thumb:
- Root blueprint stays stable and short.
- Sub-specs are focused (one domain/area each).
- Link sub-specs from this index.
- Clarify “stable core” vs “evolving extensions”.

Example structure (create these files only if/when needed):

```text
docs/specs/
  blueprint.md               # root
  definitions/
    kernel.md
    ingest.md
    retrieval.md
    observability.md
    security.md
```

## Interfaces / Contracts

- API endpoints / CLI commands: ...
- Data schemas: ...
- Event formats: ...

## Directory Overview

Keep this aligned with the real repo shape; examples:
- `src/` — ...
- `apps/` — ...
- `packages/` — ...
- `docs/` — ...

## Runbook

- Setup:
- Dev:
- Test:
- Deploy:

## Observability

- Logs:
- Metrics:
- Error taxonomy:

## Security

- Secrets handling:
- Permissions:

## Rollback Plan

How to back out changes safely.
