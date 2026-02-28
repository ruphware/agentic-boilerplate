# cdd-boilerplate

A tiny, documentation-first **template contract** for building with coding agents — KISS, but with consistently high-quality outcomes.

**Positioning:**
- **Resumable**: any agent can pick up from TODO + INDEX + JOURNAL
- **Auditable**: every step has checks + UAT
- **Safe-by-default**: PRD/Blueprint are the contract; INDEX is the context snapshot
- **Tool-agnostic**: works with a wide range of coding agents and editor/IDE integrations.

## Human-in-the-loop contract (required)

This repo is a workflow contract, not just a folder template.

**Humans must provide:**
- Product intent (what “good” means)
- Non-negotiable constraints
- Acceptance criteria
- Final sign-off via UAT

**Agents do best at:**
- Turning intent/specs into step plans
- Implementation + doc updates
- Producing exact validation commands
- Keeping changes small, consistent, and well-logged

**CDD step gate:** nothing is “done” until the human runs the step’s UAT and signs it off.

## What this is (and isn’t)

This template gives you:
- a repo-level operating contract for agents (`AGENTS.md`)
- a step-based execution plan (`TODO.md`) with **Automated checks** + **UAT** discipline
- a docs system designed for “high-density context” + change safety (`docs/*`)

This template does **not** give you:
- a tech stack, runtime, or app framework
- any bundled agent “skills” packs

## Template contract (invariants)

When you create a new repo from this template, keep these invariants true:

- **Required files:** `AGENTS.md`, `README.md`, `TODO.md`
- **Required docs:**
  - `docs/INDEX.md` (generated context snapshot)
  - `docs/JOURNAL.md` (ADR/dev journal)
  - `docs/specs/prd.md` and `docs/specs/blueprint.md` (project contract)
  - `docs/prompts/PROMPT-INDEX.md` (how to regenerate `docs/INDEX.md`)
- **Generated vs edited by hand:**
  - Regenerate: `docs/INDEX.md`
  - Edit by hand: `TODO.md`, `docs/specs/*`, `docs/JOURNAL.md`

## Why this works (KISS, but high-quality)

At any moment you can answer:
- What are we building? → PRD
- How is it structured? → Blueprint
- What’s next? → TODO
- What changed and why? → JOURNAL
- What exists right now? → INDEX

…and every step is small, testable, and gated by UAT.

## Quickstart (new repo)

### 1) Create repo from template

GitHub UI:
- Click **Use this template** → create a new repo.

GitHub CLI:
```bash
gh repo create <owner>/<new-repo> --template ruphware/cdd-boilerplate --private
# or --public

git clone git@github.com:<owner>/<new-repo>.git
cd <new-repo>
```

### 2) Replace template placeholders

Preferred:
```bash
rg -n "<PROJECT NAME>|YYYY-MM-DD|cdd-boilerplate" .
```

Fallback if `rg` isn’t installed:
```bash
grep -REIn "<PROJECT NAME>|YYYY-MM-DD|cdd-boilerplate" .
```

### 3) Fill the contract

- Fill in:
  - `docs/specs/prd.md`
  - `docs/specs/blueprint.md`
- Update `TODO.md` Step 00 to match your project.

### 4) Regenerate `docs/INDEX.md`

Use `docs/prompts/PROMPT-INDEX.md` as the canonical instruction set. Then verify Mermaid renders correctly on GitHub.

### 5) Start building

Begin Step 01 (first vertical slice) and add real **Automated checks** + **UAT**.

## Scaling conventions (optional)

### Modular blueprints

Keep `docs/specs/blueprint.md` as the root and optionally branch into focused sub-specs (by domain/area). This lets agents load only what they need.

### Multi-TODO

Some projects benefit from multiple TODOs by area.

Convention:
- Root `TODO.md` remains required.
- Optional: `TODO-<area>.md` (e.g. `TODO-backend.md`, `TODO-ios.md`).
- Root `TODO.md` should contain an “Active Work Index” linking to sub-TODOs.
- A step lives in exactly one TODO file.

## Agent workflow (no skills required)

### Agent boot prompt (paste this into any coding agent)

```text
Read AGENTS.md and follow it as the operating contract.
Read README.md, TODO.md, docs/specs/blueprint.md, docs/specs/prd.md, docs/JOURNAL.md.
Read docs/INDEX.md if present (otherwise generate it using docs/prompts/PROMPT-INDEX.md).
Work in TODO.md steps; every step must include exact automated checks + a UAT checklist.
Ask questions only if missing info would change the solution; otherwise proceed with explicit assumptions.
```

### INDEX refresh prompt (paste this into any coding agent)

```text
Open docs/prompts/PROMPT-INDEX.md and execute it verbatim.
Update docs/INDEX.md so Mermaid renders on GitHub and the file inventory matches the repo.
```

## Optional: external CDD skills (not shipped here)

This template intentionally ships **no** tool-specific skill packs so it stays stable and portable.

If you want an optional, separate skills repo, see:
- `ruphware/cdd-skills`

## License

MIT (see `LICENSE`). After templating, update the copyright holder/year.
