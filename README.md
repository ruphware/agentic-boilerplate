# CDD Boilerplate

CDD Boilerplate is a tiny, documentation-first **template contract** for building with coding agents - KISS, but with consistently high-quality outcomes.

**Core values**
- **Resumable**: any agent can pick up from TODO + INDEX + JOURNAL
- **Auditable**: every step has checks + UAT
- **Safe-by-default**: PRD/Blueprint are the contract; INDEX is the context snapshot
- **Tool-agnostic**: works with a wide range of coding agents and editor/IDE integrations.

## What you get (and what you don't)

This template gives you:
- a repo-level operating contract for agents (`AGENTS.md`)
- a step-based execution plan (`TODO.md`) with **Automated checks** + **UAT** discipline
- a docs system designed for “high-density context” + change safety (`docs/*`)

This template does **not** give you:
- a tech stack, runtime, or app framework
- any bundled agent “skills” packs

## Human-in-the-loop contract

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

## Template contract

When you create a new repo from this template, keep these invariants true:

- **Required files:** `AGENTS.md`, `README.md`, `TODO.md`
- **Required docs:**
  - `docs/INDEX.md` (generated context snapshot)
  - `docs/JOURNAL.md` (ADR/dev journal)
  - `docs/specs/prd.md` and `docs/specs/blueprint.md` (project contract)
  - `docs/prompts/PROMPT-INDEX.md` (how to regenerate `docs/INDEX.md`)
- **Fully generated vs edited:**
  - Regenerate: `docs/INDEX.md`
  - Edit: `TODO.md`, `docs/specs/*`, `docs/JOURNAL.md`

## Why this works (KISS, but high-quality)

At any moment you can answer:
- What are we building? → PRD
- How is it structured? → Blueprint
- What’s next? → TODO
- What changed and why? → JOURNAL
- What exists right now? → INDEX

…and every step is small, testable, and gated by UAT.

## Quickstart 

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

```bash
grep -REIn "<PROJECT NAME>|YYYY-MM-DD|cdd-boilerplate" .
```

### 3) Fill the contract

- Run `TODO.md` Step 00 and:
  - Fill in:
    - `docs/specs/prd.md`
    - `docs/specs/blueprint.md`
  - Use `docs/specs/prd.md` and `docs/specs/blueprint.md` to create `TODO.md` steps + tasks.
  - Update this README.md.

### 4) Start building

```text
Review and implement Step 01
```

### 5) Regenerate `docs/INDEX.md`

```text
Open docs/prompts/PROMPT-INDEX.md and execute it verbatim.
Update docs/INDEX.md so Mermaid renders on GitHub and the file inventory matches the repo.
```

## Agent boot prompt

```text
Read AGENTS.md and assume the role.
Ingest README.md, docs/specs/blueprint.md, docs/specs/prd.md to understand the project and top of docs/JOURNAL.md to get up to speed with the implementation process.
Read docs/INDEX.md if present to get an overview of the codebase.
```

## CDD Skills for Agents

This template intentionally ships **no** tool-specific skill packs so it stays stable and portable.

If you want to install Agent Skills to work with this template, see:
- [ruphware/cdd-skills](https://github.com/ruphware/cdd-skills)


## How to scale when projects get bigger?

As complexity grows, keep docs predictable and let `docs/specs/blueprint.md` route humans/agents to the right level of detail.

### Docs taxonomy (recommended)

- `docs/RUNBOOK.md`: exact dev/test/deploy commands + env vars
- `docs/specs/blueprint.md`: root spec + “Spec Index” linking to leaf specs
- `docs/specs/*-definition.md`: one subsystem per file (contracts, edge cases, tests)
- `docs/INDEX.md`: generated context snapshot (diagrams + file inventory)
- `docs/JOURNAL.md`: high-signal decisions/pitfalls (archive older entries under `docs/archive/`)
- `docs/prompts/PROMPT-INDEX.md`: canonical instructions to regenerate `docs/INDEX.md`

### Optional branching patterns (enable, don’t enforce)

- Specs: if `docs/specs/` gets large, branch into subfolders by domain (e.g. `client/`, `server/`, `ops/`) but keep `blueprint.md` as the single entrypoint.
- TODOs: keep root `TODO.md`, and optionally add `TODO-<area>.md` and/or `TODO-next.md` (backlog). If you branch TODOs, consider adding an “Active Work Index” in root `TODO.md` and keeping each step in exactly one TODO file.

Example (minimal scalable layout):
```text
docs/
  RUNBOOK.md
  INDEX.md
  JOURNAL.md
  prompts/PROMPT-INDEX.md
  specs/blueprint.md
  specs/<area>-definition.md
  archive/
TODO.md
TODO-next.md
TODO-backend.md
```

## License

Free-to-use-adjust-just-don't-blame-me-for-anything-licence. _Peace._ ✌️
