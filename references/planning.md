# Planning Playbook

Use this reference for `office-hours`, `plan-ceo-review`, `plan-eng-review`, and `plan-design-review`.

## Core Deliverables

Every planning pass should try to leave behind:

1. The actual user pain, not just the requested feature.
2. The key constraints and assumptions.
3. Two or three implementation options.
4. A recommendation with reasons.
5. A staged execution plan.
6. Risks, unknowns, and what to validate first.

## Office Hours

Push on framing:

- What pain is repeated enough that the user will care?
- What job is hidden underneath the requested feature?
- Which assumptions are probably wrong or premature?
- What is the smallest wedge that can produce learning quickly?

## CEO Review

Use one of four modes:

- Expand: the plan is too timid for the opportunity.
- Selective expansion: widen one axis, keep others tight.
- Hold scope: the plan is right-sized, execution is the real work.
- Reduce: the plan is too broad or too early.

## Engineering Review

Force the plan to specify:

- Architecture and boundaries
- Data flow and state ownership
- Failure modes and retries
- External dependencies
- Test matrix
- Observability and rollout safety
- Migration or backfill needs

## Design Review

Evaluate:

- hierarchy
- clarity
- consistency
- interaction cost
- visual distinctiveness
- responsiveness
- empty/error/loading states

When the review is weak, rewrite the plan, not just the adjectives around it.
