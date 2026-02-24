# DEV JOURNAL - Software Engineering ADR

When editing this file you act as an elite information architect. You don't like empty words, you enjoy keeping records compact, in high information density. This is a high-entropy document.

## RULES

- Add an implementation detail entry under ENTRIES.
- Focus on tricky implementation details, challenges, uncommon solutions.
- Don't duplicate basic info: TODO.md for tasks, `docs/specs/*` for specifications, `docs/INDEX.md` for the repo tree/inventory, README.md for runbook.
- Skip entries if only minor bug fixes or refactoring, documentation-only changes, test-only changes, or random config tweaks without architectural impact.
- Condense & archive: when ENTRIES >= 20, condense the oldest 15 into a single distilled summary under "SUMMARIZED (LATEST ON TOP)" with a descriptive title and the batch’s last-entry date; move the 15 originals to `docs/archive/JOURNAL_YYYY-MM-DD.md` and link to it; repeat until ≤20 remain.

**Format:**

Only use what's needed.

```
[YYYY-MM-DD HH:MM UTC]
Context: (task/area, include relevant constraints)
Decisions: (key choices & why)
Findings: (surprises, pitfalls, dead ends)
Risks: (what might break, monitoring hooks)
Important: (optional)
```

## ENTRIES (LATEST ON TOP)

[2026-02-24 11:35 UTC]
Context: Bootstrapped `agentic-boilerplate` as a GitHub Template Repository for CDD-style, agent-ready projects.
Decisions:
- Option A: repo root is the template (no duplicated templates folder).
- No "install into existing repo" bootstrap script (too many edge cases).
- MIT license.
Findings:
- Having both a root template and a `templates/` directory is confusing; removed `templates/` to keep DX clean.
Risks:
- Without a bootstrap script, adoption into existing repos is manual; mitigate by keeping the file set minimal and copy-friendly.

## SUMMARIZED (LATEST ON TOP)
