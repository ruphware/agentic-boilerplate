# TODO

> Development plan

Use this file as the current execution checklist. Keep it short and brutal.

Guidance:
- Specs live in `docs/specs/*` (PRD/Blueprint/definitions).
- Repo context lives in `docs/INDEX.md`.
- Decision log lives in `docs/JOURNAL.md`.

Archiving:
- When this TODO gets long, move completed/old sections to `docs/archive/TODO_YYYY-MM-DD.md` and leave only the active plan here.

---

## Phase 0 — Setup (day 0)

- [ ] Fill in `docs/specs/prd.md`
- [ ] Fill in `docs/specs/blueprint.md`
- [ ] Update `AGENTS.md` with repo-specific constraints (if any)
- [ ] Regenerate `docs/INDEX.md` using `docs/prompts/PROMPT-INDEX.md`

## Phase 1 — MVP

- [ ] Define MVP acceptance criteria (in PRD)
- [ ] Implement core vertical slice
- [ ] Add basic observability (logs + error taxonomy)
- [ ] Add tests for the critical path

## Phase 2 — Hardening

- [ ] Add lint/format/typecheck
- [ ] Add CI pipeline (optional)
- [ ] Add security baseline (secrets handling, least privilege, audits)
- [ ] Add backup/rollback notes (runbook)

## Phase 3 — Release

- [ ] Versioning/release process
- [ ] Deployment runbook
- [ ] On-call / ops notes (if applicable)
