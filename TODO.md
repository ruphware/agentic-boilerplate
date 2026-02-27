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

---

## Template — Step

Copy this block per step:

```
## Step <NN> — <title>

Goal:
- …

Deliverable:
- …

Changes:
- Files to add/edit: …

Automated checks:
- … (commands)

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
- (add project-specific commands here once tooling exists)

UAT:
- Open `docs/INDEX.md` and confirm diagrams render on GitHub.
- Confirm the file inventory matches the repo tree.

## Step 01 — first vertical slice (MVP)

Goal:
- Implement the smallest end-to-end slice that proves the architecture.

Deliverable:
- A running path that exercises core inputs → logic → outputs.

Changes:
- Add/edit: (project-specific)

Automated checks:
- (commands)

UAT:
- (manual checklist)
