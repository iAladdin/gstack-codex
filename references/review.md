# Review Playbook

Use this reference for `review` and as a secondary input for `ship`, `qa`, and `codex`.

## Review Order

1. Correctness and behavior regressions
2. Missing tests or broken test intent
3. Data loss / security / permission issues
4. Concurrency, lifecycle, or race problems
5. Performance cliffs
6. Maintainability only if it affects risk or future bugs

## Findings Format

Each finding should include:

- Severity or priority
- Where it lives
- The concrete failure mode
- Why it matters in real execution
- What evidence supports it

## When There Are No Findings

Say so explicitly, then mention:

- what you checked
- what you could not verify
- any residual risks

## Auto-Fix Rule

If the user asked for review only, do not silently patch.

If the user wants help landing the change and a finding is obvious and low-risk, fix it in the same turn and show the validation.
