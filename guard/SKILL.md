---
name: guard
description: Combine cautious execution with a frozen edit scope. Use when the task is risky and the user wants both confirmation on destructive actions and strict limits on which files may change.
---

# Guard

1. Read `../references/principles.md`.
2. Read `../references/safety.md`.

## Rules

- Apply `careful` and `freeze` together.
- Confirm destructive actions.
- Keep edits inside the declared boundary until the user lifts it.
