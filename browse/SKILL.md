---
name: browse
description: Use the bundled Playwright-based persistent browser for interactive QA, screenshots, authenticated flows, local sites, stateful debugging, and browser automation that web.run cannot handle.
---

# Browse

1. Read `../references/principles.md`.
2. Read `../references/browser.md`.

## Rules

- Prefer `browse` over `web.run` for local apps, auth walls, screenshots, or multi-step UI flows.
- Before first use, find the binary with `./browse/bin/find-browse` and run `./setup` if missing.
- Start with `snapshot -i`, then interact using `@e` refs.
- Include screenshot paths in your reply when visual evidence matters.
