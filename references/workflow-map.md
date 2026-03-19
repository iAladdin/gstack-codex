# Workflow Map

Use this map to route work the same way the original gstack routes a sprint.

## Think

- `office-hours`: clarify the user problem and reframe the request.

## Plan

- `plan-ceo-review`: product scope, ambition, sequencing, what not to build.
- `plan-eng-review`: architecture, interfaces, data flow, errors, migrations, tests.
- `plan-design-review`: critique a proposed UX/UI direction before code.
- `design-consultation`: generate or refine a design system from scratch.

## Build / Debug

- `investigate`: reproduce and isolate a bug before changing code.
- `browse`: drive a real browser session when local or authenticated UI matters.

## Review / Test

- `review`: code-level findings and merge readiness.
- `design-review`: visual and UX audit with fixes.
- `qa`: run browser QA and fix what you find.
- `qa-only`: run browser QA but do not modify code.
- `setup-browser-cookies`: import login cookies into the persistent browser.
- `codex`: independent second-opinion review or challenge workflow.

## Ship / Learn

- `ship`: final verification, tests, PR, release hygiene.
- `document-release`: refresh stale docs after the change.
- `retro`: summarize what shipped, what regressed, and what to improve.

## Safety

- `careful`: add confirmation and rollback thinking around risky operations.
- `freeze`: restrict edits to an agreed scope.
- `guard`: combine `careful` and `freeze`.
- `unfreeze`: remove the current scope lock.
