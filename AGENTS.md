# Project Notes For Agents

This is Roman Zhalyalov's UX/UI portfolio website. Roman is a UX/UI designer building a portfolio site from his Figma layouts. The goal is a polished static portfolio for employers, hosted on GitHub Pages and accessible without relying on Vercel.

## Model

Use **claude-sonnet-4-6** for this project. Do not ask Roman for permission before taking local actions (editing files, running builds, deleting unused assets). Confirm only before pushing to remote or other irreversible external actions.

## Current State

- First implementation pass is complete.
- Home page has gone through several visual-polish passes with Roman's feedback. It is not final pixel-perfect, but the current direction must be preserved unless Roman explicitly asks to revert it.
- The project is an Astro static site with 5 routes:
  - `/`
  - `/projects/burosfera/`
  - `/projects/quiz/`
  - `/projects/mary-trufel/`
  - `/projects/peptidy/`
- Production build has passed with `astro build` after the latest Peptid.ru page polish.
- Astro diagnostics have passed with `astro check`: 0 errors, 0 warnings, 0 hints.
- Local dev server was run at `http://127.0.0.1:4321/`.
- Git is initialized in this folder.
- GitHub remote is connected: `https://github.com/fantom9000/roman-portfolio`.
- Current branch is `main`; latest saved commit is `Polish Peptid.ru case page`.
- Latest commit: `Responsive pass + 3D tiles WebP conversion`
- Welcome section uses 5 single-image phone PNGs (1093×2223 after alpha trim), simple grid, gap 10px, max-width 1385px. Mobile: horizontal scroll at 760px.
- Concepts section rebuilt as 7-tile flex bento grid matching Figma structure (see Figma node 351-26598). All tiles exported as PNG 2x by Roman, converted to lossless WebP.
- Project preview images (burosfera, quiz, mary-trufel, peptidy) converted to lossless WebP in `public/images/figma/high/previews/`.
- **Typography system** — all font sizes live in 5 semantic CSS variables in `:root`:
  - `--type-lead`    → hero/lead text (59px at 1440px, scales to 31px)
  - `--type-section` → section headings "Задизайнил", "Законцептил" etc (42px → 21px)
  - `--type-number`  → project numbers 01–04 (80px → 48px)
  - `--type-body`    → all descriptions, welcome, side-work text (20px → 12px)
  - `--type-ui`      → nav, header, footer (fixed 20px)
  - At ≤768px, `:root` overrides: `--type-body: 20px`, `--type-section: 28px`, `--type-number: 64px`
  - Exception: `.project-sidebar h2/p` at mobile = 16px (intentional — compact layout with large number)
  - To change any role globally: edit its variable. It updates everywhere across all pages and breakpoints.
- `text-indent` on hero text fixed: uses `var(--sidebar)` percentage (was hardcoded 310px). Resets to 0 only at 760px, not at 1100px.
- Unused image folders deleted: `figma/optimized/`, `figma/exact/`, top-level `optimized/`, stale home/ originals.
- `.claude/` and `CLAUDE.md` added to `.gitignore` to prevent Claude internal files from polluting git.

## Remaining Work (home page)

- **3D tiles:** Converted from PNG to lossless WebP via Pillow (alpha trim + lossless). PNGs still exist in `public/images/figma/high/three-d-tiles/` and can be deleted after visual approval. Index.astro updated to reference `.webp`.
- **Welcome phones carousel** (desktop + mobile):
  - Desktop: removed `max-width: 1385px; margin: 0 auto` — phones now span full content width, edges align with all other page content.
  - Mobile (≤768px): full horizontal scroll carousel. Phone width = `calc((100vw - 32px) / 2.5)` — always exactly 2.5 phones visible. `margin-left/right: calc(-1 * var(--pad))` for full viewport bleed. `padding-left/right: var(--pad)` so first phone aligns to left силовая линия and last phone has same right margin as all content. `overscroll-behavior-x: contain` prevents page from scrolling when swiping phones. Scrollbar hidden (`scrollbar-width: none`, `::-webkit-scrollbar { display: none }`).
  - Project preview images: removed forced `aspect-ratio: 1.35` at mobile — images now display at their natural proportions.

- **Mobile layout pass complete** (session 2026-05-12, continued):
  - Project preview at ≤768px: kicker moved outside `.project-sidebar` in HTML → flex column with `order`: kicker (1) → visual (2) → sidebar/meta (3).
  - `.project-sidebar__meta` at mobile: CSS grid `auto 1fr`, number spans both rows (`grid-row: 1/3`), `font-size: 64px; line-height: 1` (approximates height of title+description block).
  - Project title and description at mobile: `font-size: 16px` (separate from side-work and welcome which stay at 20px).
  - Section headings at mobile (`.side-work__text h2`): `font-size: 28px` — same as `.project-kicker`. Applied to "Законцептил", "Натридешил" etc.
  - `.side-work__text` at mobile: `margin-bottom: 40px` (2× the ~20px gap from heading to divider above).
  - `.project-kicker` at mobile: `font-size: 28px; margin-bottom: 40px`.
  - Concepts bento grid and 3D grid: desktop layout preserved at mobile (full width, no column changes).
  - `--text-59` minimum kept at `31px` (not raised — higher values caused 5-line lead on narrow desktops with text-indent).
  - Number matching text height is approximated via fixed `font-size: 64px`. Pure CSS auto-matching is not possible without JS; SVG path for the number would enable exact matching but deferred.

- **Responsive pass complete** (session 2026-05-12):
  - Fluid typography: `--text-59` now viewport-proportional (`clamp(31px, 4.22vw - 1.69px, 59px)`) so the lead text holds 4 lines at all desktop widths. `--text-42` and `project-number` clamp updated to 768px base.
  - `--text-left: clamp(12px, calc(5px + 1.042vw), 20px)`: scales left-column body text (project titles, descriptions, side-work descriptions, welcome text) from 20px at 1440px down to ~13px at 769px. Clamp minimum is 12px but effectively never reached — formula hits ~13px at 768px (mobile breakpoint). Applied to: `.project-sidebar h2`, `.project-sidebar p`, `.side-work__text p`, `.welcome-work__text h2/p`.
  - `--text-42` changed to viewport-proportional formula (`clamp(21px, 3.2vw - 4px, 42px)`), same principle as `--text-59`. Maintains constant air between left-column headings and right column at all desktop widths.
  - Header/Footer restructured: `.brand`/`.footer-name` replaced with flat `.site-name` + `.site-role` elements. `.site-header` and `.site-footer` changed to `display: grid; grid-template-columns: var(--sidebar) 1fr auto` — "Дизайнер интерфейсов" now always sits exactly on the силовая линия at all desktop widths.
  - Mobile breakpoint changed from 760px to 768px throughout.
  - `three-d-tile img`: `height: 100%` → `height: auto`.
  - At ≤768px: `three-d-grid` → single column; `concepts-grid` → flex column with per-section `aspect-ratio`.
- **PNG source files** for concept tiles still exist alongside WebP — can be deleted once Roman approves quality.

## Case Pages — Layout System

All case pages use a shared component architecture:
- Each page = `<CasePage project={project} />` (one line)
- `CasePage.astro` iterates `project.sections` and renders typed components: `TextSection`, `BrowserFrame`, `ImagePair`, `MobileScreens`, `DesktopMobileScreens`, `wideImage`
- All content (text, images, section types) lives in `src/data/projects.ts`

**Силовые линии on case pages** — all visual elements align to `var(--sidebar)`:
- `TextSection`: `grid-template-columns: calc(var(--sidebar) - 20px) 62.43%` — left col scales with sidebar, right col = 62.43% for consistent right air
- `BrowserFrame` / `wideImage`: `width: min(1086px, calc(100% - var(--sidebar)))` — fills right column exactly
- `ImagePair` / `MobileScreens`: `flex: 0 0 calc((100% - var(--sidebar) - 20px) / 2)` — each tile = half of right column, proportional at all widths
- `DesktopMobileScreens`: `grid-template-columns: calc(100% - var(--sidebar) - 242px) 222px` — desktop fills right column minus phone (222px) and gap (20px)

Previously: `case-image-tile`, `mobile-screen`, and `desktop-mobile-screens` used fixed pixel widths (533px, 844px) — at viewports narrower than 1440px they drifted left past the силовая линия.

- `/projects/burosfera/` has been expanded against Figma and visually approved.
- `/projects/quiz/` uses correct Figma-derived SayGames blocks, visually approved.
- `/projects/mary-trufel/` uses correct Figma-derived blocks, visually approved.
- `/projects/peptidy/` structurally complete for desktop at 1440. Responsive and image quality deferred.

## Stack

- Astro + TypeScript + plain CSS.
- Static output for GitHub Pages.
- Do not assume Vercel as the primary hosting target.
- User is comfortable with HTML/CSS and wants the code to remain understandable.

## Important Local Commands

This machine did not have system `npm`, `pnpm`, or `yarn`. A local pnpm copy was unpacked into `.tools/pnpm`, and `.tools/` is gitignored.

Use this Node binary:

```bash
/Users/Roman/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/bin/node
```

Useful commands:

```bash
env ASTRO_TELEMETRY_DISABLED=1 /Users/Roman/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/bin/node .tools/pnpm/bin/pnpm.cjs run build
env ASTRO_TELEMETRY_DISABLED=1 /Users/Roman/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/bin/node .tools/pnpm/bin/pnpm.cjs exec astro check
env ASTRO_TELEMETRY_DISABLED=1 /Users/Roman/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/bin/node node_modules/astro/astro.js dev --host 127.0.0.1 --port 4321
```

Astro telemetry must stay disabled in sandboxed runs, otherwise Astro tries to write to `~/Library/Preferences/astro`.

Rollup native module had macOS code-signature issues in this environment. `package.json` includes a pnpm override to use `@rollup/wasm-node@4.60.3`. If build ever fails with `@rollup/rollup-darwin-arm64`, reinstall dependencies and make sure Vite resolves Rollup to the WASM package.

## Figma Source

- Main page: `https://www.figma.com/design/SKQ1C6VplMtF9IJjDELfSr/Портфолио?node-id=351-26568`
- UI-kit: `https://www.figma.com/design/SKQ1C6VplMtF9IJjDELfSr/Портфолио?node-id=365-26027`
- File key: `SKQ1C6VplMtF9IJjDELfSr`
- Main Figma routes/pages discovered:
  - `Main`
  - `Бюросфера`
  - `Квиз`
  - `Мэри Трюфель`
  - `Пептиды`
- For Figma work, use `get_design_context` and `get_metadata` when needed, but be economical with context. Roman prefers to provide page screenshots and downloaded assets himself when possible. Ask Roman for screenshots/assets instead of generating screenshots automatically unless a screenshot is essential to resolve ambiguity.

## Layout System — Силовые линии

This principle applies to ALL pages of the site. Never break it.

The layout is built on two vertical power lines (силовые линии):
- **Left line**: 20px from the left edge of the page. Everything in the left column starts here: "Роман Жалялов", project numbers, side-work headings.
- **Right line**: `--sidebar = 22.428571%` from the container. Everything in the right column starts here: "Дизайнер интерфейсов" in the header, the paragraph indent on the lead text, project visuals, concept/3D grids. This is a proportional value — it shifts left as the viewport narrows, and all content follows it.

**Scaling rules (desktop, 768px–1440px+):**
- The layout stays two-column at all desktop widths. Right column content scales proportionally.
- Left column font sizes scale DOWN as the viewport narrows (see `--text-left` variable). This is mandatory to prevent left column text from overflowing into the right column — long Russian words will break the layout otherwise.
- The lead text (лид, hero h1) should always occupy exactly 4 lines. Font size must scale proportionally with the available text-area width so line count stays constant.
- Right-column large headings (`--text-42`, `--text-59`) scale via `clamp()`.
- The sidebar percentage stays constant at all desktop widths. No fixed-pixel sidebar at any desktop breakpoint.
- There must always be visual air between left column text and the right column. `padding-right: 20px` on `.project-sidebar` and `.side-work__text` is the minimum gap.

**Breakpoints:**
- ≤768px → single-column mobile layout (the only mobile breakpoint).
- >768px → two-column desktop layout with proportional scaling.
- No breakpoints between 768px and 1440px. Everything scales fluidly via `clamp()` and percentages.

**Reference site**: https://www.erno.works/ — same editorial grid logic. Font sizes and layout scale proportionally as viewport narrows. No abrupt jumps.

**Quality standard**: This is Roman's professional portfolio. It must display perfectly at all widths, all devices, and all browsers. Visual quality is non-negotiable.

## Design Rules

- The site is an editorial UX/UI portfolio, not a marketing landing page.
- Preserve the strict grid, large visuals, restrained typography, and sparse black/white/gray palette.
- Current home-page text at 20px uses `line-height: 1.2` after Roman asked to restore Inter Display and adjust line height. Do not silently change it back.
- Do not scale font size with viewport width.
- Letter spacing should stay `0`; avoid negative tracking in CSS even if Figma export included it.
- On the home page, preserve the agreed custom sidebar treatment rather than blindly reverting to the original Figma factoids:
  - large two-digit number (`01`, `02`, etc.), currently 80px on desktop;
  - project title;
  - short description.
- Project title and description should read like one text block: title is 20px bold, description is 20px regular, with only a small line-gap-like distance between them.
- Descriptions in project preview sidebars should align visually to the lower area of the image/sidebar.
- Keep underlines only for project titles and navigation/contact elements. Do not underline descriptions or entire cards.
- Do not use the old Figma factoid treatment with logo beside a huge number unless Roman explicitly asks to restore it.
- Do not place descriptive beige text labels over project preview images on the home page.
- Browser-window chrome above screenshots is decorative and should be CSS, not a downloaded Figma asset.
- On case pages, the current approved direction removes browser-window chrome from desktop screenshots. Desktop screenshots use 12px rounded corners and a subtle shadow instead of a visible browser bar or border. Phone-background tiles and mobile screenshot tiles also use 12px corners. Do not change the rounded shape of standalone phone mockups unless Roman asks. The shared tile/screenshot CSS value is `--case-radius: 12px`.
- Some home-page choices intentionally differ from Figma:
  - no beige/gray label overlays over project preview images;
  - custom left project sidebar remains;
  - project visuals may use Figma-composition crops, but text labels inside the images should be removed/cropped rather than covered with obvious patches.
- Welcome delivery should show phone mockups, not just flat screen images.
- The 3D section should not have one big external background plate around the whole block. Use individual tiles/images so the page background remains white around the section.
- For visual assets, do not over-compress. Portfolio visuals, especially 3D, must stay vivid and sharp. Prefer high-quality PNG while polishing; optimize to high-quality WebP/AVIF later only after visual approval.

## Assets

- Figma assets are saved locally under `public/images`.
- Runtime pages must not depend on Figma API asset URLs.
- Active Figma-derived assets are under `public/images/figma/high/`:
  - `previews/` — project preview images for home page
  - `welcome/` — 5 phone mockup PNGs (single flat export per phone, transparent bg)
  - `concepts/` — concepts collage
  - `three-d-tiles/` — 3D work tiles
- `public/images/home/` contains only `quiz-1.png`, `quiz-2.png`, `quiz-3.png` (used in ProjectPreview for the quiz tile).
- Figma-derived assets for the polished Quiz case are under:
  - `public/images/projects/quiz/figma-sections`
- Quiz is approved for now. Its first and third visual rows are intentionally rendered as separate `imagePair` tiles, not single flattened wide images, so each gray tile receives the shared 12px radius from CSS.
- Figma-derived assets for the polished Mary Trufel case are under:
  - `public/images/projects/mary-trufel/figma-sections`
- Mary Trufel is approved for now. Its final two-phone row should stay a standard `imagePair` using two ready-made 533×714 Figma tile exports, not a hand-built phone mockup from separate screen/frame layers.
- Figma-derived assets for the Peptid.ru case are under:
  - `public/images/projects/peptidy/figma-sections`
- Peptid.ru desktop at 1440 is structurally approved for now. Its image quality still needs a later source/optimization pass, and responsive issues should be handled with the other pages in a shared responsive pass.
- `public/images/figma/optimized/` and `public/images/figma/exact/` have been deleted — do not reference them.
- Future improvement: generate high-quality WebP/AVIF variants from approved PNG/source assets when the dependency environment is stable.

## Code Organization

- `src/pages` contains routes.
- `src/components` contains reusable layout and portfolio components.
- `src/data` contains project copy, links, image references, and placeholder contacts.
- `src/styles/global.css` contains global CSS, grid, type, components, and responsive behavior.
- `src/data/site.ts` contains name, role, and placeholder contact links.
- `src/data/projects.ts` contains all project metadata, preview copy, page copy, routes, and image references.
- Home page layout is in `src/pages/index.astro`.
- Project preview markup is in `src/components/ProjectPreview.astro`.
- Case pages currently share data from `src/data/projects.ts`; when polishing project pages, first check whether the needed content/assets already exist there.

## Session Start Rule

When Roman brings tasks at the start of a session, **ask which task to start with** before doing anything. Do not auto-execute all tasks in sequence. Some tasks (like image replacement) have a prerequisite step on Roman's side (exporting from Figma, dropping files). Starting without confirmation means processing the wrong assets or making changes without a visual basis.

Specific mistake to never repeat: Roman described a workflow "Roman exports PNG → drops files → agent processes". There were already old PNG files in the target folder from a previous session. Instead of waiting for confirmation that fresh files had been dropped, the agent silently processed the old files. Always ask "have you dropped the new files?" before processing assets.

## Editing Guidance

- Prefer changing project names, descriptions, order, and image refs in `src/data/projects.ts`.
- Prefer changing Telegram/email/CV in `src/data/site.ts`.
- Keep `.astro` components readable for a designer who knows HTML/CSS.
- Do not blindly paste Figma-generated React/Tailwind code. Adapt it to Astro + CSS.
- Do not add Tailwind unless Roman explicitly asks.
- Do not delete existing GitHub Pages files or remote content without inspecting them first.
- Do not overwrite Roman-approved custom changes just because Figma differs. Ask or preserve the latest agreed direction.
- For page-polish tasks, compare, while minimizing context use:
  - Figma screenshot/metadata;
  - local browser screenshot at 1440px;
  - actual asset quality in `public/images`.
- Prefer asking Roman to provide screenshots for visual comparison. Do not generate your own browser/Figma screenshots unless explicitly needed or requested.
- If an image looks bad, inspect whether it is a low-resolution export, over-compressed WebP, or a broken transparent/black Figma asset before changing layout.
- Before claiming completion, run:

```bash
env ASTRO_TELEMETRY_DISABLED=1 /Users/Roman/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/bin/node .tools/pnpm/bin/pnpm.cjs run build
env ASTRO_TELEMETRY_DISABLED=1 /Users/Roman/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/bin/node .tools/pnpm/bin/pnpm.cjs exec astro check
```

## Known Follow-Ups

- Continue visual review with Roman in the browser.
- Main page still needs final visual review, especially exact vertical rhythm and responsive behavior, but current custom direction should be preserved.
- Peptid.ru page polish is structurally complete for desktop at 1440. Do not reopen its structure unless Roman asks.
- Later, revisit image quality across the site. Roman may export higher-quality final images from Figma; prefer approved sharp source assets before final optimization.
- Before final publishing, do a typography pass for non-breaking spaces, hanging prepositions, punctuation, ruble signs, and responsive line breaks.
- Check responsive layouts at 1440, 1024, 768, and 390 px.
- Add real Telegram, email, and CV links later.
- Inspect Roman's existing `fantom9000.github.io` setup before publishing if the desired URL is `https://fantom9000.github.io/` without a repository subfolder.
