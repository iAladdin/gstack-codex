# Investigation Playbook

Use this reference for `investigate`.

## Iron Law

Do not “fix” until you can explain the failure mode in plain language.

## Investigation Loop

1. Reproduce the issue.
2. Capture evidence: logs, stack traces, state, screenshots, or failing tests.
3. Narrow the boundary where behavior diverges from expectation.
4. Form the smallest hypothesis that explains the evidence.
5. Test the hypothesis.
6. Only then change code.
7. Add or update a regression test when feasible.

## Escalate When

- The issue has been “fixed” multiple times without a stable explanation.
- The bug depends on missing external systems you cannot access.
- You cannot distinguish app behavior from tooling or environment failure.
