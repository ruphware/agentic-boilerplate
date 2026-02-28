# TODO

This file is the active execution plan.

Rules:
- Write work as **steps**.
- Every step must include:
  - **Automated checks** (exact commands: lint/typecheck/tests/build)
  - **UAT** (manual acceptance checklist)
- Keep it current; archive aggressively.

Archiving:
- When the file becomes long/noisy, move completed sections to `docs/archive/TODO_YYYY-MM-DD.md`.

Multi-TODO (optional):
- Keep this file as the root plan.
- If you add sub-TODOs, add an **Active Work Index** section in this file linking to them.
- Optional additional TODOs are allowed: `TODO-<area>.md` (one step lives in exactly one TODO file).

---

## Template — Step

Copy this block per step.

Required headings: Goal / Deliverable / Changes / Automated checks / UAT.

```md
## Step <NN> — <title>

Goal:
- …

Deliverable:
- …

Confirm (optional):
- Acceptance rules / behavior constraints to lock before implementation.

Plan (optional):
- File plan: `filename | purpose | ≈LOC`
- Logging plan: 3–7 grep-friendly logs at key state changes / I/O.
- Risks: top likely failure modes.

Implementation tasks (optional):
- [ ] …

Tests (optional):
- Unit:
- Integration:

Changes:
- Files to add/edit: …

Automated checks:
- … (exact commands)

UAT:
- … (manual checklist)
```

---

## Step 00 — project setup

Goal:
- Establish the project contract and repo context.

Deliverable:
- Filled-in PRD + Blueprint and a generated INDEX.

Changes:
- Edit: `docs/specs/prd.md`
- Edit: `docs/specs/blueprint.md`
- Generate/update: `docs/INDEX.md`

Automated checks:
- test -f docs/specs/prd.md && test -f docs/specs/blueprint.md
- test -f docs/INDEX.md
- ! grep -REIn "<PROJECT NAME>|YYYY-MM-DD" docs/specs/*.md

UAT:
- Open `docs/INDEX.md` and confirm diagrams render on GitHub.
- Confirm the file inventory matches the repo tree.

## Next: create Step 01 (project-specific)

After Step 00 is done, add your own Step 01 using the template above.
Do not proceed without filling **Automated checks** (exact commands) and **UAT** (manual checklist).

---
