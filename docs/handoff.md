# Current Handoff

This file is the short transition note for moving work between Codex, Claude Code, and manual editing. For full project rules, read `AGENTS.md`.

## Last Known Stable State

- Branch: `main`
- Remote: `https://github.com/fantom9000/roman-portfolio`
- Latest saved commit noted in project instructions: `Polish Peptid.ru case page`
- Build status noted in project instructions: passed after the latest Peptid.ru polish
- Astro check status noted in project instructions: 0 errors, 0 warnings, 0 hints

## Current Product Direction

- This is an editorial UX/UI portfolio, not a marketing landing page.
- Preserve the strict grid, large visuals, restrained typography, and sparse black/white/gray palette.
- Figma is a reference source, not an automatic override. Several implemented decisions intentionally differ from Figma after Roman's feedback.
- The home page has a Roman-approved custom project sidebar direction and should not be blindly reverted to the original Figma factoid layout.
- The Burosfera, Quiz, Mary Trufel, and Peptid.ru case pages have approved current structures.
- Peptid.ru is structurally approved at 1440px desktop; responsive and image-quality polish are deferred to a shared later pass.

## Do Not Change Without Explicit Approval

- Do not add Tailwind.
- Do not introduce a Vercel dependency.
- Do not change home-page text back from 20px / `line-height: 1.2` / `letter-spacing: 0`.
- Do not restore old Figma factoids with logo beside a huge number.
- Do not add beige/gray text labels over home-page preview images.
- Do not add browser-window chrome back to case-page desktop screenshots. "Browser chrome" means decorative browser UI around the screenshot: top bar, traffic-light dots, address bar, fake browser frame, or visible browser window header.
- Do not change the shared `--case-radius: 12px` direction unless Roman asks.
- Do not replace approved sharp source assets with over-compressed images.

## Figma Access Expectations

Claude Code only sees Figma if Figma MCP/design tools are connected in that Claude Code environment, or if Roman provides screenshots/exported assets. If Figma tools are unavailable, the agent must say so and ask Roman for the exact screenshot, node link, or asset export needed.

When Figma tools are available:

1. Use the exact frame/node link when possible.
2. Fetch only the needed node/frame.
3. Compare against the current site and approved deviations in `AGENTS.md`.
4. Do not silently revert approved site decisions to match Figma.
5. Ask Roman if the correct choice is ambiguous.

## Likely Next Work

1. Site-wide responsive pass at 1440, 1024, 768, and 390 px.
2. Site-wide image-quality pass using approved source assets or Roman-provided exports.
3. Typography pass for non-breaking spaces, hanging prepositions, punctuation, ruble signs, and responsive line breaks.
4. Final publishing checks for GitHub Pages.

## Required Verification

Run these before saying the work is complete:

```bash
env ASTRO_TELEMETRY_DISABLED=1 /Users/Roman/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/bin/node .tools/pnpm/bin/pnpm.cjs run build
env ASTRO_TELEMETRY_DISABLED=1 /Users/Roman/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/bin/node .tools/pnpm/bin/pnpm.cjs exec astro check
```

## Recommended Cross-Agent Setup

Use a separate branch or worktree for Claude Code:

```bash
git worktree add ../roman-portfolio-claude -b claude/responsive-pass main
```

Use Codex and Claude Code on different branches or worktrees when possible. Avoid letting both agents edit `src/styles/global.css`, `src/data/projects.ts`, `src/pages/index.astro`, or `src/components/ProjectPreview.astro` at the same time.
