---
name: setup-browser-cookies
description: Import login cookies from a local Chromium-based browser into the persistent QA browser. Use when authenticated pages block QA, the user wants to test a logged-in flow, or local/staging auth needs to be reused safely.
---

# Setup Browser Cookies

1. Read `../references/principles.md`.
2. Read `../references/browser.md`.

## Flow

- Ensure the `browse` binary exists.
- Use `cookie-import-browser` to inspect installed browsers or import directly for a domain.
- Prefer the narrowest domain import needed for the task.
- Re-run `snapshot -i` after import to verify the logged-in state.
