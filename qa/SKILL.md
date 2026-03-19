---
name: qa
description: Run end-to-end QA with a real browser and fix what you find. Use when the user wants browser testing, regression reproduction, staging verification, form-flow testing, or authenticated/local UI QA with follow-up fixes.
---

# QA

1. Read `../references/principles.md`.
2. Read `../references/browser.md`.
3. Use `../references/review.md` for reporting format.

## Rules

- Prefer the bundled `browse` binary for interactive verification.
- Check screenshots, console errors, network failures, and end state.
- If you fix a bug, re-verify the flow and add a regression test when feasible.
