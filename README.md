# cdd-boilerplate

A documentation-first **template contract** for Chat-Driven Development (CDD): the minimum repo shape that makes work with coding agents predictable, auditable, and easy to resume.

## What this is (and isn’t)

This template gives you:
- a repo-level operating contract for agents (`AGENTS.md`)
- a step-based execution plan (`TODO.md`) with **checks + UAT** discipline
- a docs system designed for “high-density context” + change safety (`docs/*`)

This template does **not** give you:
- a tech stack, runtime, or app framework
- any bundled agent “skills” packs

If you want optional Codex skills, install them separately from `ruphware/cdd-skills` (explicit-only). The template works without skills.

## Template contract (invariants)

When you create a new repo from this template, these are the invariants you keep true:

- **Required files:** `AGENTS.md`, `README.md`, `TODO.md`
- **Required docs:**
  - `docs/INDEX.md` (generated context snapshot)
  - `docs/JOURNAL.md` (ADR/dev journal)
  - `docs/specs/prd.md` and `docs/specs/blueprint.md` (project contract)
  - `docs/prompts/PROMPT-INDEX.md` (how to regenerate `docs/INDEX.md`)
- **Generated vs edited by hand:**
  - Regenerate: `docs/INDEX.md`
  - Edit by hand: `TODO.md`, `docs/specs/*`, `docs/JOURNAL.md`
## What you get

- `AGENTS.md` — agent operating rules (CDD) + output format + DoD
- `TODO.md` — step plan template; every step has **Automated checks** + **UAT**
- `docs/specs/` — PRD + Blueprint templates (project contract)
- `docs/INDEX.md` — generated repo context snapshot (architecture + inventory + diagrams)
- `docs/JOURNAL.md` — high-signal dev journal / ADR log with archive rules
- `docs/prompts/PROMPT-INDEX.md` — canonical instructions for regenerating `docs/INDEX.md`

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

## Agent workflow (no skills required)

### Agent boot prompt (paste this into any coding agent)

```text
Read AGENTS.md and follow it as the operating contract.
Read README.md, TODO.md, docs/specs/blueprint.md, docs/specs/prd.md, docs/INDEX.md, docs/JOURNAL.md.
Work in TODO.md steps; every step must include exact automated checks + a UAT checklist.
Ask questions only if missing info would change the solution; otherwise proceed with explicit assumptions.
```

### INDEX refresh prompt (paste this into any coding agent)

```text
Open docs/prompts/PROMPT-INDEX.md and execute it verbatim.
Update docs/INDEX.md so Mermaid renders on GitHub and the file inventory matches the repo.
```

## Optional: external CDD skills (not shipped here)

If you use Codex CLI and want explicit-only skills, install them from:
- `ruphware/cdd-skills`

This template is intentionally skill-free so it stays stable and tool-agnostic.

## License

MIT (see `LICENSE`). After templating, update the copyright holder/year.
