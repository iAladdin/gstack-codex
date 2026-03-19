---
name: gstack-codex
description: Codex-native software factory modeled after gstack. Route product discovery, plan review, code review, debugging, browser QA, shipping, documentation, retros, and safety workflows to the right sibling skill. Use when the user asks for a gstack-style workflow, software factory, office hours, plan review, QA, shipping, or wants help choosing which workflow skill to use.
---

# gstack-codex

This is the router skill for the repository.

## Start Here

1. Read `references/principles.md` for default operating rules.
2. Read `references/workflow-map.md` to pick the correct sibling skill.
3. Prefer the sibling skill over improvising a new workflow when the request clearly matches one.

## Routing Guide

- Idea still fuzzy, user pain not yet sharp: use `office-hours/`
- Strategic scope or founder-level product judgment: use `plan-ceo-review/`
- Architecture, interfaces, data flow, failure modes, tests: use `plan-eng-review/`
- Design quality before implementation: use `plan-design-review/`
- Design exploration or design system creation: use `design-consultation/`
- Code review, regression hunting, merge readiness: use `review/`
- Root-cause debugging before fixing: use `investigate/`
- Visual polish or frontend audit with fixes: use `design-review/`
- End-to-end QA with browser interaction: use `qa/`
- Browser QA report only, no edits: use `qa-only/`
- Release prep, tests, PR, ship checklist: use `ship/`
- Docs sync after changes: use `document-release/`
- Sprint or weekly reflection: use `retro/`
- Interactive browser automation, screenshots, local app verification: use `browse/`
- Cookie import for authenticated QA: use `setup-browser-cookies/`
- Independent second opinion inside Codex: use `codex/`
- Risk-sensitive task requiring extra guardrails: use `careful/`, `freeze/`, `guard/`, `unfreeze/`

## Codex-Specific Notes

- Use `web.run` for public-web research and citations.
- Use the bundled `browse` binary for local URLs, authenticated apps, screenshots, and multi-step UI flows.
- Use subagents only when the user explicitly wants delegation, a second opinion, or parallel work.
