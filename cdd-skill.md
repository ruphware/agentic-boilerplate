# CDD Skill Pack (Chat‑Driven Development) — create + publish guide

This document tells you exactly how to package **Chat‑Driven Development (CDD)** as **explicit‑only Agent Skills** for **Codex CLI** (and keep the pack compatible with other skill-aware CLI agents).

**Key property:** these skills are **explicit-only**. They must be invoked via `$skill-name`. They will not trigger automatically.  
(Implemented via `agents/openai.yaml` → `policy.allow_implicit_invocation: false`.)  
See: OpenAI Codex “Agent Skills” docs.

---

## 1) Recommended repo naming + description

### 1.1 Rename repo: `agentic-boilerplate` → `cdd-boilerplate`
Rationale:
- “CDD” is the brand + the method (Chat‑Driven Development).
- “boilerplate” still fits, but it’s a methodology + skill pack.

GitHub UI steps:
1. Repo → **Settings** → **General** → **Repository name**
2. Rename to `cdd-boilerplate`
3. Suggested description:
   - **“Chat‑Driven Development (CDD): agentic development methodology + Codex skill pack.”**

After renaming, GitHub redirects most existing URLs automatically (issues, stars, etc.).  
(If someone later creates a new repo at the old path, redirects may no longer apply.)

Local git remote update:
```bash
git remote -v
git remote set-url origin https://github.com/<OWNER>/cdd-boilerplate.git
git remote -v
```

---

## 2) What we’re building

We will add a skill pack under:

- **Repo skills:** `.agents/skills/<skill-name>/...`

Each skill is a directory with a required `SKILL.md`, plus optional:
- `assets/` (templates/resources)
- `scripts/` (tiny deterministic helpers)
- `references/` (extra docs)
- `agents/openai.yaml` (UI metadata + invocation policy + tool deps)

Codex discovers skills by scanning `.agents/skills` from your current folder up to the repo root.  
It also discovers user-wide skills in `~/.agents/skills`. Symlinks are supported.

---

## 3) Create the directories

From the repo root:

```bash
mkdir -p .agents/skills/cdd-ship-step/{assets,scripts,references,agents}
mkdir -p .agents/skills/cdd-refresh-index/{assets,scripts,references,agents}
```

Optional (recommended) docs folder if you don’t already have it:
```bash
mkdir -p docs/prompts
```

---

## 4) Make skills explicit-only (MANDATORY)

### File: `.agents/skills/cdd-ship-step/agents/openai.yaml`
```yaml
interface:
  display_name: "CDD: ship a TODO step"
  short_description: "Plan → patch → checks → report, aligned to AGENTS.md + TODO.md"
policy:
  allow_implicit_invocation: false
```

### File: `.agents/skills/cdd-refresh-index/agents/openai.yaml`
```yaml
interface:
  display_name: "CDD: refresh docs/INDEX.md"
  short_description: "Regenerate architecture snapshot + inventory using PROMPT-INDEX"
policy:
  allow_implicit_invocation: false
```

**Why this works:** `allow_implicit_invocation` defaults to true; when false, Codex will not implicitly select the skill, but explicit `$skill` invocation still works.

---

## 5) Add the skills

### 5.1 Skill: `cdd-ship-step`

#### File: `.agents/skills/cdd-ship-step/SKILL.md`
```md
---
name: cdd-ship-step
description: |
  EXPLICIT-ONLY SKILL.
  Use this skill only when explicitly invoked via `$cdd-ship-step`.

  Primary use:
  - Implement a concrete change (feature/bugfix/refactor) and produce a working patch.
  - Create or update a TODO.md step with:
    - Automated checks (exact commands)
    - UAT checklist
  - Follow the repo’s operating contract in AGENTS.md.

  Don’t use when:
  - The user wants only Q&A, brainstorming, or review without code changes.
  - The task is only to refresh docs/INDEX.md (use `$cdd-refresh-index`).

  Success criteria:
  - Minimal patch implementing the deliverable.
  - TODO step has Goal/Deliverable/Changes/Automated checks/UAT.
  - Validation commands listed (and run when possible).
  - Final report includes files changed + commands + next action.
---

# CDD Ship Step Skill (explicit-only)

## 0) Repo contract (required)
1) Read and follow `/AGENTS.md` (repo-level contract).
2) Read: `/TODO.md`, `/docs/INDEX.md`, `/docs/JOURNAL.md`, and any relevant `/docs/specs/*`.

If `docs/INDEX.md` is missing/stale and the task depends on architecture context:
- Prefer running `$cdd-refresh-index` explicitly before continuing.

## 1) Plan before edits (required)
Provide:
- **File Plan** table: `filename | purpose | ≈LOC`
- **Logging Plan:** 3–7 grep-friendly logs at key branches/state changes/I/O
- **Risks:** list likely failure points (interfaces, migration, data shape, env assumptions)

## 2) Implementation constraints (required)
- Keep changes minimal; avoid unrelated refactors.
- Do not remove existing logs/tests unless explicitly requested.
- Prefer composition over cleverness.
- Add logs where state changes or branching occurs.

## 3) TODO step discipline (required)
If the work is not represented in TODO.md:
- Add a new `## Step NN — ...` section using the template in:
  `.agents/skills/cdd-ship-step/assets/todo-step.template.md`

Every step MUST include:
- Goal
- Deliverable
- Changes
- Automated checks (exact commands)
- UAT checklist

## 4) Validate (required)
Run repo checks if they exist (lint/typecheck/tests/build).
If checks don’t exist, propose exact commands and capture missing checks as a follow-up TODO step.

## 5) Documentation updates (required when applicable)
Update:
- `docs/JOURNAL.md` when changes are non-trivial (decisions, trade-offs, gotchas).
- `docs/INDEX.md` (or run `$cdd-refresh-index`) when architecture/inventory materially changes.

## 6) Final report format (required)
Return:
- GOAL (1 sentence)
- CONSTRAINTS (bullets)
- METHOD (2–4 lines)
- ASSUMPTIONS
- EXECUTION (files changed + key decisions)
- VALIDATION (exact commands)
- NEXT (commit message + next step)
```

#### File: `.agents/skills/cdd-ship-step/assets/todo-step.template.md`
```md
## Step NN — <title>

Goal:
- …

Deliverable:
- …

Changes:
- Files to add/edit: …
- Key interfaces impacted: …

Automated checks:
- … (exact commands)

UAT:
- … (manual acceptance checklist)
```

#### File: `.agents/skills/cdd-ship-step/assets/journal-entry.template.md`
```md
## YYYY-MM-DD — <short title>

Context:
- Why this change was needed.

Decision:
- What we decided to do.

Options considered:
- A) ...
- B) ...

Notes / gotchas:
- Sharp edges, migrations, rollback notes.

Validation:
- Commands run:
  - ...
- Manual checks (UAT):
  - ...
```

#### Optional deterministic script (recommended)
Use scripts sparingly: instructions first; scripts only for deterministic enforcement.

File: `.agents/skills/cdd-ship-step/scripts/validate_todo.py`
```python
#!/usr/bin/env python3
"""
validate_todo.py — deterministic TODO.md structure checker for CDD.

Usage:
  python .agents/skills/cdd-ship-step/scripts/validate_todo.py [path/to/TODO.md]

Checks:
- Each "## Step" section includes: Goal, Deliverable, Changes, Automated checks, UAT

Exit codes:
- 0: OK
- 1: Validation failed
- 2: File not found / unreadable
"""

from __future__ import annotations

import re
import sys
from dataclasses import dataclass
from pathlib import Path
from typing import List, Tuple

STEP_HEADER_RE = re.compile(r"^##\s+Step\b.*$", re.MULTILINE)

REQUIRED_FIELDS = [
    "Goal:",
    "Deliverable:",
    "Changes:",
    "Automated checks:",
    "UAT:",
]

@dataclass(frozen=True)
class StepIssue:
    step_heading: str
    missing_fields: List[str]

def _log(level: str, event: str, **fields: str) -> None:
    kv = " ".join([f'{k}="{v}"' for k, v in fields.items()])
    print(f"[CDDValidateTodo] {level} {event} {kv}".strip(), file=sys.stderr)

def _split_steps(todo_text: str) -> List[Tuple[str, str]]:
    headers = list(STEP_HEADER_RE.finditer(todo_text))
    steps: List[Tuple[str, str]] = []
    for i, m in enumerate(headers):
        start = m.start()
        end = headers[i + 1].start() if i + 1 < len(headers) else len(todo_text)
        block = todo_text[start:end].strip()
        heading = m.group(0).strip()
        steps.append((heading, block))
    return steps

def validate(todo_path: Path) -> List[StepIssue]:
    if not todo_path.exists():
        raise FileNotFoundError(str(todo_path))

    text = todo_path.read_text(encoding="utf-8", errors="strict")
    steps = _split_steps(text)
    _log("INFO", "ParsedSteps", steps=str(len(steps)))

    issues: List[StepIssue] = []
    for heading, block in steps:
        missing = [f for f in REQUIRED_FIELDS if f not in block]
        if missing:
            issues.append(StepIssue(step_heading=heading, missing_fields=missing))
    return issues

def main(argv: List[str]) -> int:
    todo_path = Path(argv[1]) if len(argv) > 1 else Path("TODO.md")
    try:
        issues = validate(todo_path)
    except FileNotFoundError:
        _log("ERROR", "TodoNotFound", path=str(todo_path))
        return 2
    except Exception as e:
        _log("ERROR", "TodoReadFailed", path=str(todo_path), msg=str(e))
        return 2

    if not issues:
        _log("INFO", "TodoValid", path=str(todo_path))
        return 0

    for issue in issues:
        _log(
            "ERROR",
            "StepMissingFields",
            step=issue.step_heading,
            missing=",".join(issue.missing_fields),
        )
    return 1

if __name__ == "__main__":
    raise SystemExit(main(sys.argv))
```

---

### 5.2 Skill: `cdd-refresh-index`

This skill should wrap your repo’s `docs/prompts/PROMPT-INDEX.md` contract.

#### File: `.agents/skills/cdd-refresh-index/SKILL.md`
```md
---
name: cdd-refresh-index
description: |
  EXPLICIT-ONLY SKILL.
  Use this skill only when explicitly invoked via `$cdd-refresh-index`.

  Use when:
  - docs/INDEX.md is missing/stale or repo has materially changed.
  - You need an updated architecture snapshot + file inventory.

  Don’t use when:
  - The primary goal is code changes (use `$cdd-ship-step`).

  Success criteria:
  - Update docs/INDEX.md with GitHub-safe Mermaid and LOC inventory.
  - Change ONLY docs/INDEX.md unless PROMPT-INDEX explicitly requires more.
---

# CDD Refresh Index Skill (explicit-only)

## Canonical instructions
- Execute `/docs/prompts/PROMPT-INDEX.md` as the source of truth.

## Rules
- Update ONLY `docs/INDEX.md` unless PROMPT-INDEX requires otherwise.
- Use shell commands to compute LOC + inventories.
- Keep Mermaid compatible with GitHub Markdown.
```

---

## 6) Verify Codex discovers the skills

From any folder inside the repo:
1) Run Codex interactive and type `$` or `/skills` to see skills.
2) If an update doesn’t appear, restart Codex (Codex detects skill changes automatically, but restart is the fallback).

If two skills share the same `name`, Codex does not merge them; both can appear.

---

## 7) Use from terminal (Codex CLI)

### 7.1 Interactive (TUI)
- Type `$` or run `/skills`
- Select the skill
- Give the task prompt

### 7.2 Non-interactive (`codex exec`) — for CI and scripts
Important behaviors:
- While running, Codex streams progress to `stderr` and prints the final message to `stdout`.
- By default `codex exec` runs in a read-only sandbox.
- Use `--full-auto` to allow edits in automation.
- Use `--json` to emit a JSONL event stream to stdout (great for evals).
- Use `--output-schema` for a final JSON that matches a schema.
- Use `-o`/`--output-last-message` to write the final assistant message to a file.

Examples:

Run a CDD ship step (edits enabled):
```bash
codex exec --full-auto \
  '$cdd-ship-step Implement TODO Step NN. Keep changes minimal. Include Automated checks + UAT.'
```

Refresh INDEX (only docs/INDEX.md should change):
```bash
codex exec --full-auto \
  '$cdd-refresh-index Refresh docs/INDEX.md using docs/prompts/PROMPT-INDEX.md. Only change docs/INDEX.md.'
```

Capture trace events for evaluation:
```bash
codex exec --json --full-auto \
  '$cdd-ship-step Add Step NN to TODO.md with Automated checks + UAT' \
  > /tmp/cdd-trace.jsonl
```

### 7.3 Authentication (quick reference)
Codex supports browser OAuth by default; for API keys you can use:
```bash
printenv OPENAI_API_KEY | codex login --with-api-key
```

---

## 8) Testing (minimum viable, repeatable)

### 8.1 Smoke tests (manual)
Run each skill on a small task and check:
- git status only includes expected files
- TODO step contains required sections
- validation commands are plausible and complete

### 8.2 Trace-based evals (recommended)
Create a small folder `evals/cdd/` and keep prompts + expectations.

Minimal approach (no custom harness):
1) Create prompts:
   - `evals/cdd/prompts.txt` with one prompt per line (explicit invocations only)
2) Run:
```bash
while IFS= read -r p; do
  echo "=== $p ==="
  codex exec --json --full-auto "$p" > "evals/cdd/trace.$(date +%s).jsonl"
done < evals/cdd/prompts.txt
```
3) Grade:
- files changed (git status in a worktree or fresh clone)
- number of command executions in JSONL
- TODO step validator script result:
```bash
python .agents/skills/cdd-ship-step/scripts/validate_todo.py TODO.md
```

If you want isolation, use `git worktree` per prompt (recommended for non-flaky evals).

---

## 9) Publish to GitHub

```bash
git add cdd-skill.md .agents/skills
git commit -m "add explicit-only CDD skill pack for codex"
git push origin main
```

Optional: tag releases so teams can pin skill versions:
```bash
git tag -a v0.1.0 -m "initial CDD skill pack"
git push --tags
```

---

## 10) Optional: install globally (for use in any repo)

Codex reads user skills from:
- `~/.agents/skills`

Clone your repo somewhere stable:
```bash
git clone https://github.com/<OWNER>/cdd-boilerplate.git ~/src/cdd-boilerplate
```

Symlink skills:
```bash
mkdir -p ~/.agents/skills

ln -sf ~/src/cdd-boilerplate/.agents/skills/cdd-ship-step ~/.agents/skills/cdd-ship-step
ln -sf ~/src/cdd-boilerplate/.agents/skills/cdd-refresh-index ~/.agents/skills/cdd-refresh-index
```

Update later:
```bash
cd ~/src/cdd-boilerplate && git pull
```

### Disable a skill without deleting it (optional)
Codex supports disabling a skill via config entries:
- `~/.codex/config.toml` with `[[skills.config]] ... enabled = false`

(Useful for temporarily turning off a skill pack.)

---

## 11) Optional: compatibility notes (other agents)

Other tools may look in:
- Project: `.github/skills` or `.claude/skills`
- User: `~/.copilot/skills` or `~/.claude/skills`

If you want max portability, you can symlink the same skill folders into those locations.

---

## 12) Troubleshooting

### Skill not visible in `/skills`
- Confirm the folder is under `.agents/skills/<name>/SKILL.md`
- Confirm `SKILL.md` has YAML frontmatter with `name:` and `description:`
- Restart Codex (it usually auto-detects, restart is the fallback)

### Skill triggers implicitly (should not happen)
- Confirm `.agents/skills/<skill>/agents/openai.yaml` contains:
  - `policy.allow_implicit_invocation: false`
- Confirm you are running a Codex version that supports invocation policy in `agents/openai.yaml`

### Conflicting skill names
- If two skills share the same `name`, Codex will not merge them. Rename one.

---

## 13) References (recommended reading)
- OpenAI Codex — Agent Skills: https://developers.openai.com/codex/skills/
- OpenAI Codex — Non-interactive mode (`codex exec`): https://developers.openai.com/codex/noninteractive/
- OpenAI Codex — CLI reference: https://developers.openai.com/codex/cli/reference/
- GitHub Docs — Renaming a repository: https://docs.github.com/en/repositories/creating-and-managing-repositories/renaming-a-repository
- GitHub Copilot — Creating agent skills: https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/create-skills
