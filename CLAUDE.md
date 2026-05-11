# Claude Project Instructions

Before making changes, read `AGENTS.md` and `docs/handoff.md`.

This is Roman Zhalyalov's UX/UI portfolio website. Roman is a UX/UI designer building a polished static portfolio from Figma layouts for employers. The site is hosted through GitHub Pages and must not depend on Vercel.

## Working Rules

- Preserve the current approved design direction unless Roman explicitly asks to change it.
- Figma is an important source, but it is not the only source of truth. Some current site decisions intentionally differ from Figma after Roman's feedback.
- Never "fix" the site back to Figma when `AGENTS.md` or `docs/handoff.md` says the current deviation is approved.
- Do not rewrite the project structure.
- Do not add Tailwind or a new styling framework.
- Keep the code understandable for a designer who knows HTML/CSS.
- Prefer focused edits in `src/data/projects.ts`, `src/data/site.ts`, Astro components, and `src/styles/global.css`.
- Do not use runtime Figma API asset URLs. Runtime assets must live under `public/images`.
- Ask before changing approved case-page structure or reverting Roman-approved custom home-page choices.
- If the Figma MCP/tools are not connected in Claude Code, say that directly and ask Roman for screenshots or exported assets. Do not pretend to have inspected Figma.
- Before claiming completion, run the verification commands from `AGENTS.md` or use `/portfolio-verify`.

## Figma Usage

Figma file:

- Main page: `https://www.figma.com/design/SKQ1C6VplMtF9IJjDELfSr/Портфолио?node-id=351-26568`
- UI kit: `https://www.figma.com/design/SKQ1C6VplMtF9IJjDELfSr/Портфолио?node-id=365-26027`
- File key: `SKQ1C6VplMtF9IJjDELfSr`

When a task requires Figma comparison:

1. Use Figma MCP/design tools if they are available in the Claude Code session.
2. Fetch only the exact needed node/frame, not the whole file.
3. Compare Figma against the current implemented site and the approved deviations in `AGENTS.md`.
4. If Figma conflicts with an approved deviation, preserve the implemented direction and ask Roman before changing it.
5. If Figma access is not configured, ask Roman for a screenshot or exported asset.

Approved deviations from Figma include, but are not limited to:

- Home page keeps the custom project sidebar with a large two-digit number, project title, and short description.
- Home page does not use beige/gray text labels over project preview images.
- Home page does not restore the old Figma factoid layout with a logo beside a huge number.
- Case-page desktop screenshots do not use "browser chrome": no decorative browser top bar, no address bar, no browser dots, no fake window frame above the screenshot.
- Case-page desktop screenshots use the approved clean image treatment: 12px rounded corners and a subtle shadow.
- The shared tile/screenshot radius is `--case-radius: 12px`.

## First Response In A New Session

When starting work in this repository, briefly confirm that you have read:

1. `AGENTS.md`
2. `docs/handoff.md`
3. `src/data/projects.ts` if the task touches projects, copy, images, or case pages
4. `src/styles/global.css` if the task touches layout, typography, responsive behavior, or visual polish

Then summarize only the relevant current constraints before editing.

## Recommended Workflow

Use Git as the source of truth.

- Work on a separate branch for Claude Code changes, for example `claude/responsive-pass`.
- Keep `main` as the last stable branch.
- Commit coherent checkpoints before switching back to Codex.
- Before handoff, use `/portfolio-handoff` and update `docs/handoff.md` if the project state changes.

## When Unsure

Ask Roman a focused question instead of guessing. This is especially important for:

- Whether to follow Figma or preserve an approved site deviation.
- Whether an asset is sharp enough for final portfolio use.
- Whether a responsive compromise is acceptable.
- Whether a case-page structure should be changed.
