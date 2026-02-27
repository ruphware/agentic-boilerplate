# cdd-boilerplate

Chat‑Driven Development (CDD): agentic development methodology + Codex skill pack.

This is a GitHub **template repository** you can fork/template for new projects.

## What you get

This template standardizes the minimum set of files that make a repo easy to operate with coding agents:

- `AGENTS.md` — the **agent prompt** for this repo (instructions for coding agents; humans can read it, but it’s written for agents)
- `TODO.md` — step-based plan; **each step should include automated checks + UAT**
- `docs/specs/*` — PRD/Blueprint/definition specs (the contract)
- `docs/INDEX.md` — periodically generated high-density repo context (architecture + inventory + diagrams)
- `docs/prompts/*` — prompts used for repo maintenance (includes INDEX refresh prompt)
- `docs/JOURNAL.md` — high-signal dev journal / ADR log with strict archive rules

## Quickstart (new project)

### GitHub UI
- Click **Use this template** → create a new repo.

### GitHub CLI
```bash
gh repo create <owner>/<new-repo> --template ruphware/cdd-boilerplate --private
# or --public
```

## RENAME CHECKLIST (DO THIS FIRST)

Right after templating:

1) **Update identity strings**
- `README.md` title + description
- `docs/specs/prd.md` and `docs/specs/blueprint.md`: replace `<PROJECT NAME>` and `YYYY-MM-DD`

2) **Search for template placeholders**
```bash
rg -n "<PROJECT NAME>|YYYY-MM-DD|cdd-boilerplate" .
```

3) **Regenerate repo context**
- Update `docs/INDEX.md` to match the real codebase using `docs/prompts/PROMPT-INDEX.md`.

## Agent workflow (boot prompt)

Copy/paste this as the repo boot prompt:

```text
Ingest AGENTS.md and assume the role.
Read README.md docs/INDEX.md docs/specs/blueprint.md to understand the project.
See top of docs/JOURNAL.md for implementation process and details.
```

## INDEX refresh workflow

Copy/paste this when you want a fresh `docs/INDEX.md`:

```text
We have new developments, and we need you to diligently create new index for our codebase:
- Ingest @docs/prompts/PROMPT-INDEX.md and execute the prompt verbatim!
- Use the correct tools to count the lines and fulfill all the requirements, including updating the diagrams and keeping the Mermaid syntax compatible with GitHub.
```

## License

MIT (see `LICENSE`).
