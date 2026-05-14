---
name: typograf
description: Run Russian typograf on all source text. Use when Roman asks "прогони типограф", "запусти типограф", "/typograf", or when text content was added/edited in src/data/*.ts or src/**/*.astro and needs non-breaking spaces, em-dashes, ёлочка-quotes applied. Also runs automatically before `pnpm build`.
---

# Typograf

Запускает npm-пакет `typograf` (русский) на всех `.ts` и `.astro` файлах в `src/`. Вставляет настоящие Unicode-символы (неразрывный пробел U+00A0, длинное тире, кавычки-ёлочки и т.д.) — НЕ HTML-сущности.

Команда:

```bash
env ASTRO_TELEMETRY_DISABLED=1 /Users/Roman/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/bin/node .tools/pnpm/bin/pnpm.cjs typograf
```

Или эквивалентно:

```bash
node scripts/typograf.mjs
```

Что обрабатывается:
- Строки в кавычках с кириллицей: атрибуты типа `text="..."`, `alt="..."`, `aria-label="..."`, поля в `src/data/*.ts`
- Текст между тегами `<p>`, `<h1>-<h6>`, `<li>` если содержит кириллицу

Что НЕ обрабатывается:
- Строки в JS-выражениях `{...}` внутри Astro
- Строки без кириллицы (пути, имена классов и т.д.)

Запускается автоматически перед `pnpm build` через `prebuild` хук.

После запуска: всегда проверь визуально что текст не сломался и неразрывные пробелы стоят там, где нужно.
