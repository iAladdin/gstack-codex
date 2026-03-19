---
name: codex
description: Run an independent second-opinion workflow inside Codex. Use when the user explicitly wants a second opinion, adversarial review, independent plan critique, or asks to delegate an extra review pass to another agent.
---

# Codex Second Opinion

1. Read `../references/principles.md`.
2. Read `../references/review.md`.

## Rules

- Only use subagents when the user explicitly wants delegation, a second opinion, or parallel review.
- Keep the delegated prompt narrow and independent.
- Use the subagent result as evidence, not as a replacement for your own judgment.

## Modes

- Review: independent findings-only diff review
- Challenge: try to break assumptions or edge cases
- Consult: focused question on architecture or implementation
