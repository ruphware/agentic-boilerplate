# TODO

> Active execution plan (steps). Gate completion on Automated checks + UAT.

Reference: `docs/specs/prd.md` and `docs/specs/blueprint.md`.
Archive: move completed steps to `docs/archive/TODO_YYYY-MM-DD.md` when noisy.
Note: Regenerate `docs/INDEX.md` once there’s code/structure worth snapshotting (use `docs/prompts/PROMPT-INDEX.md`).

---

## Step 00 — project setup

Goal:
- Establish the project contract (PRD + Blueprint) and a project-specific README.

Tasks:
- [ ] Fill in `docs/specs/prd.md` (replace `<PROJECT NAME>` / `YYYY-MM-DD`; add goals + acceptance criteria).
- [ ] Fill in `docs/specs/blueprint.md` (replace placeholders; add architecture + runbook).
- [ ] Update `README.md` using newly created `docs/specs/prd.md` and `docs/specs/blueprint.md`.

Automated checks:
- test -f docs/specs/prd.md && test -f docs/specs/blueprint.md && test -f README.md
- ! grep -REIn "<PROJECT NAME>|YYYY-MM-DD" docs/specs/*.md README.md

UAT:
- [ ] Confirm no placeholders remain.

---

## Step template (copy/paste)

```md
## Step <NN> — <title>

Goal:
- …

Tasks:
- [ ] …

Automated checks:
- …

UAT:
- [ ] …
```
