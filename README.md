# gstack-codex

[中文说明](README.zh-CN.md)

`gstack-codex` is a Codex-native software factory inspired by the workflow design of `gstack`, but adapted to how Codex actually works: trigger-based skills, local tooling, subagents when explicitly requested, `web.run` for current research, and a persistent Playwright browser for real UI QA.

It gives you two things:

- A workflow stack: product reframing, plan review, code review, investigation, browser QA, shipping, documentation, and retros.
- A browser stack: a fast persistent `browse` binary for screenshots, auth flows, local apps, staging verification, and stateful debugging.

This is not a thin rename of the original repo. The Claude slash-command model has been reworked into a Codex skill pack, while the strongest implementation idea from the original project, the persistent browser daemon, stays intact.

## Who This Is For

- Founders and solo builders who want a repeatable AI-native development workflow
- Staff engineers and tech leads who want stronger review, QA, and release discipline
- Codex users who do not want to start every task from a blank prompt
- Anyone who wants real browser QA instead of “I think this page should work”

## Quick Start

1. Install the skill pack into `~/.codex/skills/gstack-codex`
2. Run `./setup`
3. Open any project in Codex
4. Start with one of these prompts:

```text
Use office-hours to help me sharpen this product idea: I want to build a daily briefing app for my calendar and email.
```

```text
Use review to inspect the current changes and give me findings first.
```

```text
Use qa to test http://localhost:3000, verify the login flow, and fix anything broken.
```

## Install

Requirements:

- Codex
- Git
- Bun 1.x+
- macOS if you want local Chromium cookie import

### Install Globally

```bash
git clone <your-repo-url> ~/.codex/skills/gstack-codex
cd ~/.codex/skills/gstack-codex
./setup
```

What `setup` does:

- installs dependencies
- builds `browse/dist/browse`
- installs Playwright Chromium if needed
- registers sibling skills into `~/.codex/skills/`

### Ask Codex To Install It For You

Codex can use reusable skills installed under `~/.codex/skills/`, and this repository is structured to match that model.

If you want Codex to do the install from a GitHub repository for you, paste something like this:

```text
Install gstack-codex for me from GitHub.

1. Clone <your-repo-url> into ~/.codex/skills/gstack-codex
2. Run ./setup inside that directory
3. Verify that the sibling skills are linked under ~/.codex/skills/
4. Confirm that browse is available
5. Tell me exactly what changed
```

If you also want Codex to set up the current project to use the skill pack more intentionally, use this version:

```text
Install gstack-codex for me from GitHub and configure this workspace to use it well.

1. Clone <your-repo-url> into ~/.codex/skills/gstack-codex
2. Run ./setup there
3. Verify the installed skills and browse binary
4. Inspect this repo and add or update AGENTS.md only if a short note would make skill usage clearer
5. Tell me how I should invoke the main workflows in this project
```

Replace `<your-repo-url>` with the actual GitHub repository URL.

### Keep A Working Repo Somewhere Else

If your real source repo lives outside `~/.codex/skills/gstack-codex`, that is fine. This repository includes a sync helper:

```bash
bin/sync-install
```

That command:

- syncs the current working tree into `~/.codex/skills/gstack-codex`
- excludes local build/runtime artifacts
- runs `setup` inside the installed copy

You can also target a custom install path:

```bash
bin/sync-install /some/other/path/gstack-codex
```

## How To Invoke Skills In Codex

This is a Codex skill pack, not a Claude slash-command pack.

Use prompts like:

```text
Use office-hours to help me rethink this feature.
```

```text
Use plan-eng-review to review this implementation plan.
```

```text
Use browse to open http://localhost:3000 and show me the interactive elements.
```

Do not use:

```text
/office-hours
/qa
/ship
```

## See It Work

```text
You:    Use office-hours to help me shape an AI assistant for calendar prep.

Codex:  Pushes back on the framing, extracts the real user pain,
        identifies the hidden "chief of staff" job, proposes 3
        approaches, and recommends the narrowest wedge.

You:    Use plan-ceo-review on that direction and cut the first version down.

Codex:  Reduces the scope, keeps the highest-learning slice, and
        names what should not be built yet.

You:    Use plan-eng-review and turn that into an implementation plan.

Codex:  Locks architecture, data flow, failure modes, interfaces,
        migration concerns, and a test strategy.

You:    Use review to inspect my current branch.

Codex:  Gives findings first, calls out regressions and missing tests.

You:    Use qa to test http://localhost:3000 and fix whatever breaks.

Codex:  Opens the persistent browser, walks the flow, checks console
        and network, patches issues, and re-verifies.

You:    Use ship to confirm this is release-ready.

Codex:  Runs the right checks, makes remaining risks explicit, and
        prepares a clean shipping summary.
```

That is the core idea: not “one giant prompt,” but a sprint-shaped workflow.

## The Sprint

`gstack-codex` is designed around:

**Think → Plan → Build → Review → Test → Ship → Reflect**

The skills are meant to be used in that order:

- `office-hours` sharpens the problem
- `plan-*` forces product, engineering, and design decisions into the open
- `investigate` explains failures before code changes
- `review` catches regressions before merge
- `qa` verifies real behavior in a real browser
- `ship` handles release readiness
- `document-release` and `retro` close the loop

## Skill Directory

| Skill | Role | What It Does | Example Prompt |
|------|------|--------------|----------------|
| `gstack-codex` | Router | Chooses the right workflow when you are not sure where to start. | `Use gstack-codex to tell me whether this task needs office-hours, plan review, or QA.` |
| `office-hours` | Product discovery partner | Reframes fuzzy ideas into real user pain, hidden jobs, and better wedges. | `Use office-hours to sharpen this idea: an AI daily briefing app for calendar and email.` |
| `plan-ceo-review` | Founder / CEO | Challenges scope, ambition, sequencing, and what not to build. | `Use plan-ceo-review to cut this feature plan down to a smarter first version.` |
| `plan-eng-review` | Engineering lead | Reviews architecture, interfaces, data flow, failure modes, and tests. | `Use plan-eng-review to audit this implementation plan, especially the data flow and test strategy.` |
| `plan-design-review` | Design critic | Pressure-tests a UX/UI plan before implementation. | `Use plan-design-review to review this dashboard plan for hierarchy, clarity, and mobile behavior.` |
| `design-consultation` | Design partner | Builds a concrete visual direction, system, and component rules. | `Use design-consultation to define a visual system for this AI writing app.` |
| `review` | Staff engineer reviewer | Reviews code and diffs with findings-first output. | `Use review to inspect the current changes and give me findings first.` |
| `investigate` | Debugger | Reproduces, narrows, and explains bugs before fixes. | `Use investigate to find the root cause of users being redirected back to login after sign-in.` |
| `design-review` | Designer who ships | Audits an implemented UI and fixes the most important issues. | `Use design-review on http://localhost:3000/settings and fix the most obvious design problems.` |
| `qa` | QA lead | Runs browser QA, fixes issues, and re-verifies. | `Use qa to test the signup and login flows on http://localhost:3000 and fix what breaks.` |
| `qa-only` | QA reporter | Same depth of QA, but no code changes. | `Use qa-only to test the checkout flow on staging and give me only a bug report.` |
| `ship` | Release engineer | Checks release readiness, tests, and shipping hygiene. | `Use ship to tell me whether this branch is ready to ship.` |
| `document-release` | Technical writer | Updates docs so they match the shipped behavior. | `Use document-release to refresh the README and setup docs for the latest auth changes.` |
| `retro` | Engineering manager | Summarizes what shipped, what hurt, and what to improve next. | `Use retro to summarize this sprint and call out test and process gaps.` |
| `browse` | Persistent browser operator | Opens real pages, captures screenshots, drives auth flows, and inspects UI state. | `Use browse to open http://localhost:3000, list the interactive elements, and capture a screenshot.` |
| `setup-browser-cookies` | Session manager | Imports login cookies from local Chromium-based browsers. | `Use setup-browser-cookies to import Chrome cookies for app.example.com into browse.` |
| `codex` | Second-opinion reviewer | Runs an explicitly independent review or challenge workflow. | `Use codex for a second-opinion review of the current diff, focusing on edge cases.` |
| `careful` | Safety mode | Adds blast-radius and rollback thinking around risky actions. | `Use careful for this production migration and confirm before any destructive command.` |
| `freeze` | Scope lock | Restricts edits to one area. | `Use freeze and limit this task to apps/web/src/settings.` |
| `guard` | Safety + scope lock | Combines `careful` and `freeze`. | `Use guard for this payments fix: only touch the payments module and confirm risky commands first.` |
| `unfreeze` | Scope unlock | Removes the current edit restriction. | `Use unfreeze so broader changes are allowed again.` |

## The Browser Layer

The most concrete implementation inside this repository is the `browse` stack.

Why it matters:

- local apps like `http://localhost:3000` are testable
- authenticated pages are testable
- multi-step UI flows are testable
- screenshots and console/network evidence are easy to collect
- the browser stays warm between commands, so QA is fast

Typical browser prompts:

```text
Use browse to open http://localhost:3000 and show me the interactive elements.
```

```text
Use qa to test the login flow on http://localhost:3000 and fix anything broken.
```

```text
Use setup-browser-cookies to import Chrome cookies for staging.example.com.
```

## How This Differs From The Original gstack

- No Claude slash commands
- No dependency on Claude-specific `AskUserQuestion` or `CLAUDE.md` flows
- Browser research uses `web.run` for public sites and `browse` for real interaction
- `codex` is no longer a wrapper around the external Codex CLI by default; in this version it is a Codex-native “independent second opinion” workflow
- `careful`, `freeze`, `guard`, and `unfreeze` are scoped to Codex task behavior rather than long-lived Claude session state

## Repository Layout

| Path | Purpose |
|------|---------|
| `SKILL.md` | Router skill for the whole pack |
| `references/` | Shared principles and playbooks |
| `<skill>/SKILL.md` | One skill per workflow |
| `browse/` | Persistent Playwright browser implementation |
| `bin/` | Setup, sync, and helper scripts |
| `BROWSER.md` | Browser command reference and implementation notes |

## Development

```bash
bun install
bun run build
```

The browser runtime state is written to `.gstack-codex/` in the current project root.

## Troubleshooting

**Skills not showing up?**

```bash
cd ~/.codex/skills/gstack-codex
./setup
```

**Need to refresh the installed copy after local edits?**

```bash
bin/sync-install
```

**`browse` not available?**

```bash
~/.codex/skills/gstack-codex/browse/bin/find-browse
```

If that fails, rerun:

```bash
cd ~/.codex/skills/gstack-codex
./setup
```

## License

MIT.
