# Browser Playbook

Use this reference for `browse`, `qa`, `qa-only`, `design-review`, and `setup-browser-cookies`.

## When To Use `browse`

Prefer the bundled browser over `web.run` when you need:

- local URLs like `http://localhost:3000`
- authenticated flows
- multi-step form interaction
- screenshots from the actual running app
- DOM/stateful debugging across several actions

## Locate The Binary

```bash
BROWSER_FIND="${CODEX_HOME:-$HOME/.codex}/skills/gstack-codex/browse/bin/find-browse"
B="$("$BROWSER_FIND" 2>/dev/null || true)"
```

If that returns nothing, look for:

- workspace-local: `.codex/skills/gstack-codex/browse/dist/browse`
- global: `${CODEX_HOME:-$HOME/.codex}/skills/gstack-codex/browse/dist/browse`

If the binary is still missing, run:

```bash
${CODEX_HOME:-$HOME/.codex}/skills/gstack-codex/setup
```

## High-Value Commands

```bash
$B goto http://localhost:3000
$B snapshot -i
$B fill @e3 "user@example.com"
$B click @e4
$B screenshot /tmp/after-login.png
$B console --errors
$B network
$B cookie-import-browser chrome --domain app.example.com
```

## Reporting Screenshots

When you save a screenshot, include the local file path in the final reply with Markdown image syntax if the user would benefit from seeing it.

## Good QA Defaults

- Start with `snapshot -i`
- Re-snapshot after major DOM changes
- Check `console --errors` and `network`
- Prefer assertions plus screenshots, not screenshots alone
