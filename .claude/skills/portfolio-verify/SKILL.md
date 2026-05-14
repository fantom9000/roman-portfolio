---
description: Run the required verification commands for Roman's Astro portfolio before claiming work is complete.
---

# Portfolio Verify

Run these commands from the project root:

```bash
env ASTRO_TELEMETRY_DISABLED=1 /Users/Roman/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/bin/node .tools/pnpm/bin/pnpm.cjs run build
env ASTRO_TELEMETRY_DISABLED=1 /Users/Roman/.cache/codex-runtimes/codex-primary-runtime/dependencies/node/bin/node .tools/pnpm/bin/pnpm.cjs exec astro check
```

Report:

- Whether `build` passed or failed.
- Whether `astro check` passed or failed.
- Any exact error that still needs attention.

If either command fails because of the change you just made, fix the issue before claiming completion.

