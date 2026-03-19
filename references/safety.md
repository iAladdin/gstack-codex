# Safety Playbook

Use this reference for `careful`, `freeze`, `guard`, and `unfreeze`.

## Codex Limitation

Unlike the original gstack slash-command environment, Codex does not keep a dedicated skill session alive across turns. Treat these guardrails as:

- strongest for the current task
- optionally persisted only if the user explicitly asks for a marker or config change

## careful

Before risky actions:

- restate the operation
- name the blast radius
- name the rollback path
- ask for confirmation if the command is destructive or production-facing

## freeze

Define an allowed edit scope:

- one directory
- one package
- one set of files

If work outside the scope becomes necessary, stop and ask before editing there.

## guard

Apply both:

- `careful` confirmation rules
- `freeze` edit-scope rules

## unfreeze

Explicitly clear the current scope lock before broadening changes.
