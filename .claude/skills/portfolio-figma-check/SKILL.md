---
description: Use when a task asks to compare this portfolio against Figma, inspect Figma nodes, or decide whether to follow Figma or the approved implemented site.
---

# Portfolio Figma Check

Read before using Figma:

- `AGENTS.md`
- `CLAUDE.md`
- `docs/handoff.md`

## Figma Source

- Main page: `https://www.figma.com/design/SKQ1C6VplMtF9IJjDELfSr/Портфолио?node-id=351-26568`
- UI kit: `https://www.figma.com/design/SKQ1C6VplMtF9IJjDELfSr/Портфолио?node-id=365-26027`
- File key: `SKQ1C6VplMtF9IJjDELfSr`

## Required Behavior

- Use Figma MCP/design tools if they are available in this Claude Code environment.
- Fetch only the exact requested frame/node. Do not pull the whole file unless the task truly needs it.
- If Figma tools are not available, say that clearly and ask Roman for a screenshot, node link, or exported asset.
- Do not pretend to have inspected Figma if you only read local files.
- Compare Figma with the current implementation and the approved deviations in `AGENTS.md`.
- If Figma conflicts with an approved implemented decision, preserve the implemented direction and ask Roman before changing it.

## Known Approved Deviations

- Home page keeps the custom project sidebar with a large two-digit number, project title, and short description.
- Home page does not use beige/gray text labels over project preview images.
- Home page does not restore the old Figma factoid layout with a logo beside a huge number.
- Case-page desktop screenshots do not use browser chrome.
- "Browser chrome" means decorative browser UI around a screenshot: top bar, traffic-light dots, address bar, fake browser frame, or visible browser window header.
- Case-page screenshots use clean image treatment with `--case-radius: 12px`, 12px rounded corners, and subtle shadow where currently implemented.

## Output

When reporting a Figma comparison, say:

- What Figma node/frame was inspected.
- What the current site does.
- Whether the difference is an approved deviation or a likely issue.
- What change you recommend, if any.

