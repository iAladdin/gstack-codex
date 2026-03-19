---
name: browse
description: Use the bundled Playwright-based persistent browser for interactive QA, screenshots, authenticated flows, local sites, stateful debugging, and browser automation that web.run cannot handle.
---

# Browse

1. Read `../references/principles.md`.
2. Read `../references/browser.md`.

## Rules

- Prefer `browse` over `web.run` for local apps, auth walls, screenshots, or multi-step UI flows.
- Before first use from an arbitrary project directory, find the installed binary with `${CODEX_HOME:-$HOME/.codex}/skills/gstack-codex/browse/bin/find-browse` and rerun `${CODEX_HOME:-$HOME/.codex}/skills/gstack-codex/setup` if it is missing.
- Start with `snapshot -i`, then interact using `@e` refs.
- Include screenshot paths in your reply when visual evidence matters.
