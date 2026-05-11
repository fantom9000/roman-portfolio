---
description: Summarize current repository changes before switching work between Claude Code, Codex, and manual editing.
---

# Portfolio Handoff

Inspect the current repository state:

```bash
git status --short --branch
git diff --stat
git diff
```

Then produce a concise handoff with:

- Current branch.
- Files changed.
- What changed in plain language.
- Whether verification was run.
- Remaining risks or open decisions.
- Suggested next step.

If the project state changed meaningfully, update `docs/handoff.md` with the new stable state, current focus, and any new constraints Roman approved.

