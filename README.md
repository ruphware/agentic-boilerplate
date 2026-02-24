# agentic-boilerplate

A reusable, opinionated template set for **agentic / CDD-style software development**.

This repo exists to make new projects immediately “agent-ready” by standardizing:
- `AGENTS.md` — how coding agents should operate in this repo
- `TODO.md` — execution plan / backlog
- `docs/INDEX.md` — high-density architecture/context snapshot
- `docs/prompts/PROMPT-INDEX.md` — how to regenerate `docs/INDEX.md`
- `docs/specs/*` — PRD/Blueprint/specs as the canonical contract
- `docs/JOURNAL.md` — decision log

## Quickstart (new project)

This repo is intended to be used as a **GitHub Template Repository**.

### GitHub UI
- Click **Use this template** → create a new repo.

### GitHub CLI
```bash
gh repo create <owner>/<new-repo> --template myelin-com/agentic-boilerplate --private
# or --public
```

Then:
1. Edit `README.md` and `docs/specs/*` to reflect the new project.
2. Keep `AGENTS.md` as the operational contract for coding agents.
3. Regenerate/update `docs/INDEX.md` using `docs/prompts/PROMPT-INDEX.md` whenever structure changes.

## Structure

- `AGENTS.md` — CDD rules for agents and humans
- `TODO.md` — task list; should reference specs and runbook
- `docs/INDEX.md` — architecture overview + inventory + diagrams
- `docs/prompts/` — prompts used to generate/refresh documentation
- `docs/specs/` — PRD + blueprint + definition specs
- `docs/JOURNAL.md` — implementation log / ADRs

## Notes

- This repo contains **templates** (not a framework). It should stay language-agnostic.
- If you want language-specific additions, add them under `templates/<lang>/...`.
