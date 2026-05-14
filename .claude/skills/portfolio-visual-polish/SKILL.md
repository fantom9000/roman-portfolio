---
description: Use when polishing Roman's UX/UI portfolio visuals, responsive layout, typography, image quality, or Figma-derived sections.
---

# Portfolio Visual Polish

Before editing, read:

- `AGENTS.md`
- `CLAUDE.md`
- `docs/handoff.md`

If the task touches project data, case pages, preview text, image references, or routes, also read `src/data/projects.ts`.

If the task touches spacing, typography, responsive behavior, previews, or case-page presentation, also read `src/styles/global.css`.

## Rules

- Preserve Roman-approved visual direction unless Roman explicitly asks to change it.
- Treat Figma as a reference, not an automatic override. Some deviations from Figma are approved product decisions.
- If Figma conflicts with `AGENTS.md`, `CLAUDE.md`, or `docs/handoff.md`, preserve the approved implemented direction and ask Roman before changing it.
- Adapt Figma ideas to Astro + plain CSS; do not paste React/Tailwind output.
- Do not add Tailwind.
- Do not add Vercel-specific assumptions.
- Runtime images must live under `public/images`; do not depend on Figma API asset URLs.
- Prefer small focused changes over rewrites.
- Keep `.astro` markup readable for a designer comfortable with HTML/CSS.
- Ask Roman for screenshots/assets when visual ambiguity matters and the existing files are not enough.
- If Figma MCP/design tools are unavailable, say so explicitly and ask Roman for screenshots or exports instead of guessing.

## Visual Constraints

- Editorial UX/UI portfolio, not a marketing landing page.
- Strict grid, large visuals, restrained type, sparse black/white/gray palette.
- Home-page 20px text uses `line-height: 1.2` and `letter-spacing: 0`.
- Keep the custom home-page sidebar direction: large two-digit number, project title, short description.
- Keep underlines only for project titles and navigation/contact elements.
- Do not place beige/gray labels over preview images.
- Case-page desktop screenshots use the approved no-browser-chrome direction with `--case-radius: 12px`.
- "Browser chrome" means decorative browser UI around a screenshot: top bar, traffic-light dots, address bar, fake browser frame, or visible browser window header.

## Figma Comparison Flow

When Figma comparison is needed:

1. Use Figma MCP/design tools if available.
2. Fetch only the exact required frame/node.
3. Compare it with the current local page and the approved deviations listed in `AGENTS.md`.
4. Implement only the requested change.
5. If the change would undo an approved deviation, ask Roman first.

Before final response, use `/portfolio-verify` or run the verification commands from `AGENTS.md`.
