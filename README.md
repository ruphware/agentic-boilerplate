# agentic-boilerplate

A reusable, opinionated template repo for **agentic / Chat‑Driven‑Development (CDD)** software engineering.

This template makes new repos immediately “agent-ready” by standardizing:
- `AGENTS.md` — operating contract for coding agents (and humans)
- `TODO.md` — execution plan / backlog
- `docs/INDEX.md` — high-density architecture/context snapshot
- `docs/prompts/PROMPT-INDEX.md` — how to regenerate `docs/INDEX.md`
- `docs/specs/*` — PRD/Blueprint/specs as the canonical contract
- `docs/JOURNAL.md` — high-signal implementation journal + ADR-style decisions

## Quickstart (new project)

This repo is intended to be used as a **GitHub Template Repository**.

### GitHub UI
- Click **Use this template** → create a new repo.

### GitHub CLI
```bash
gh repo create <owner>/<new-repo> --template myelin-com/agentic-boilerplate --private
# or --public
```

## RENAME CHECKLIST (DO THIS FIRST)

Right after templating:

1) **Update obvious identity strings**
- `README.md` title + description
- `docs/specs/prd.md` and `docs/specs/blueprint.md`: replace `<PROJECT NAME>` and `YYYY-MM-DD`
- If the project has a product name separate from repo name: write both explicitly in README/PRD.

2) **Search for placeholders / template strings**
```bash
rg -n "<PROJECT NAME>|YYYY-MM-DD|agentic-boilerplate" .
```
Fix every hit.

3) **Regenerate repo context**
- Update `docs/INDEX.md` to match the real codebase using `docs/prompts/PROMPT-INDEX.md`.

4) **Decide tooling + guardrails early** (prevents churn)
- language/runtime (Node/Python/Go/etc)
- formatter/linter/typecheck/test runner
- CI baseline (optional)

## Structure

- `AGENTS.md` — CDD rules for agents and humans
- `TODO.md` — task list; should reference specs and runbook
- `docs/INDEX.md` — architecture overview + inventory + diagrams
- `docs/prompts/` — prompts used to generate/refresh documentation
- `docs/specs/` — PRD + blueprint + definition specs
- `docs/JOURNAL.md` — implementation log / ADRs

## Notes

- This repo is **the template** (Option A). We intentionally avoid a second `templates/` copy to reduce confusion.
- We intentionally do **not** include a bootstrap script for “install into existing repos” (too many edge cases). If you need that later, we can add it as a separate tool/repo.
