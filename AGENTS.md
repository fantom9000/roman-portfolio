# Project Notes For Agents

This is Roman Zhalyalov's UX/UI portfolio website. Roman is a UX/UI designer building a portfolio site from his Figma layouts. The goal is a polished static portfolio for employers, hosted on GitHub Pages and accessible without relying on Vercel.

## Current State

- First implementation pass is complete.
- Home page has gone through several visual-polish passes with Roman's feedback. It is not final pixel-perfect, but the current direction must be preserved unless Roman explicitly asks to revert it.
- The project is an Astro static site with 5 routes:
  - `/`
  - `/projects/burosfera/`
  - `/projects/quiz/`
  - `/projects/mary-trufel/`
  - `/projects/peptidy/`
- Production build has passed with `astro build` after the latest case-page screenshot polish.
- Astro diagnostics have passed with `astro check`: 0 errors, 0 warnings, 0 hints.
- Local dev server was run at `http://127.0.0.1:4321/`.
- Git is initialized in this folder.
- GitHub remote is connected: `https://github.com/fantom9000/roman-portfolio`.
- Current branch is `main`; latest saved commit is `Refine case study screenshots`.
- `/projects/burosfera/` has been expanded against Figma and visually approved as a good direction.
- Next focus: polish `/projects/quiz/`.

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
- For Figma work, use `get_design_context`, `get_metadata`, and screenshots from the Figma MCP. Compare with browser screenshots at 1440px wide before making strong visual claims.

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
- On case pages, the current approved direction removes browser-window chrome from desktop screenshots. Desktop screenshots use 12px rounded corners and a subtle shadow instead of a visible browser bar or border. Phone-background tiles also use 12px corners.
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
- Optimized JPEG copies are under `public/images/optimized`.
- Originals are kept under `public/images/home` and `public/images/projects` as source material for future re-optimization.
- Higher-quality Figma-derived assets for the current home-page polish are under:
  - `public/images/figma/high/previews`
  - `public/images/figma/high/welcome`
  - `public/images/figma/high/concepts`
  - `public/images/figma/high/three-d-tiles`
- Older compressed or experimental Figma assets may still exist under `public/images/figma/optimized` and `public/images/figma/exact`. Check image quality before using them.
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

## Editing Guidance

- Prefer changing project names, descriptions, order, and image refs in `src/data/projects.ts`.
- Prefer changing Telegram/email/CV in `src/data/site.ts`.
- Keep `.astro` components readable for a designer who knows HTML/CSS.
- Do not blindly paste Figma-generated React/Tailwind code. Adapt it to Astro + CSS.
- Do not add Tailwind unless Roman explicitly asks.
- Do not delete existing GitHub Pages files or remote content without inspecting them first.
- Do not overwrite Roman-approved custom changes just because Figma differs. Ask or preserve the latest agreed direction.
- For page-polish tasks, compare:
  - Figma screenshot/metadata;
  - local browser screenshot at 1440px;
  - actual asset quality in `public/images`.
- If an image looks bad, inspect whether it is a low-resolution export, over-compressed WebP, or a broken transparent/black Figma asset before changing layout.
- Before claiming completion, run:

```bash
env ASTRO_TELEMETRY_DISABLED=1 /Users/Roman/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/bin/node .tools/pnpm/bin/pnpm.cjs run build
env ASTRO_TELEMETRY_DISABLED=1 /Users/Roman/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/bin/node .tools/pnpm/bin/pnpm.cjs exec astro check
```

## Known Follow-Ups

- Continue visual review with Roman in the browser.
- Main page still needs final visual review, especially exact vertical rhythm and responsive behavior, but current custom direction should be preserved.
- Continue project-page polishing with the Квиз page:
  - read Figma page/context for `Квиз`;
  - compare current `/projects/quiz/` with Figma;
  - preserve readable Astro/CSS code;
  - use local assets, not remote Figma URLs;
  - verify with build/check.
- Later, revisit image quality across the site. Roman may export higher-quality final images from Figma; prefer approved sharp source assets before final optimization.
- Before final publishing, do a typography pass for non-breaking spaces, hanging prepositions, punctuation, ruble signs, and responsive line breaks.
- Check responsive layouts at 1440, 1024, 768, and 390 px.
- Add real Telegram, email, and CV links later.
- Inspect Roman's existing `fantom9000.github.io` setup before publishing if the desired URL is `https://fantom9000.github.io/` without a repository subfolder.
