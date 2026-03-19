# Principles

These rules apply across all `gstack-codex` skills.

## 1. Evidence First

- Verify before claiming success.
- When code changes, run the smallest meaningful validation available.
- If validation is blocked, say exactly what was blocked and what remains unverified.

## 2. Complete The Lake

- Prefer the complete solution when the remaining work is a bounded “lake”.
- Include tests, error handling, and edge cases when the added scope is small relative to the task.
- Explicitly call out “ocean” work that should not be silently absorbed.

## 3. Ask Only When Risk Is Real

- Default to making reasonable assumptions and moving forward.
- Ask the user only when the choice changes architecture, external behavior, safety, or significant time cost.
- If you ask, make it concrete and easy to answer.

## 4. Use The Right Surface

- `web.run`: public websites, up-to-date facts, citations.
- `exec_command`: repo inspection, local commands, tests, build tooling.
- `spawn_agent`: only when the user explicitly wants delegation, parallel work, or an independent pass.
- `browse`: local apps, screenshots, auth flows, stateful multi-step browser QA.

## 5. Findings Before Summary

For reviews, QA reports, and audits:

- Lead with bugs, regressions, or risks.
- Keep summaries short and secondary.
- Reference files, commands, and evidence tightly.

## 6. Be Honest About Codex Limits

- Codex skills are trigger-based, not slash-command sessions.
- Guardrail skills such as `freeze` and `guard` are strongest within the current task unless the user explicitly asks for a persisted marker file or config update.
- If a workflow depends on missing local tools, stop early and say what is missing.
