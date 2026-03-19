# Release Playbook

Use this reference for `ship`, `document-release`, and `retro`.

## Ship

Before claiming release readiness:

1. Sync on the correct base branch.
2. Run tests that match the changed area.
3. Review the diff for generated noise or accidental files.
4. Confirm docs or contracts changed with the code.
5. Prepare the PR summary around user-visible impact and risk.

## Document Release

Update the docs that would mislead the next engineer if left stale:

- README
- architecture docs
- setup instructions
- API or environment docs
- runbooks / testing notes

Only edit docs that are actually affected by the shipped change.

## Retro

A useful retro covers:

- what shipped
- where time or confidence was lost
- defect patterns
- test gaps
- next process improvement
