---
name: standard-sdd-debt
description: Use after implementation to capture accepted non-blocking Standard SDD follow-up work in docs/debt, including deferred tests, monitoring, migration, docs, cleanup, or risks accepted by a Review Gate.
---

# Standard SDD Debt

Goal: capture accepted non-blocking follow-up work after implementation.

Debt is not a place to hide required fixes.

## Capture Debt When

- A non-blocking issue was explicitly accepted.
- A workaround was intentionally shipped.
- Test, monitoring, migration, docs, or cleanup work was deferred.
- ADR/plan risks produced follow-up work.
- Review Gate passed with accepted residual work.

## Do Not Capture As Debt

- failing tests
- unresolved acceptance criteria
- unclear requirements
- required fixes for the selected task
- bugs that must be fixed before completion

## Process

1. Resolve the related workflow from `specs/index.md` when possible.
2. Use `templates/debt-template.md` or `templates/debt-template.zh-CN.md`.
3. Create or update `docs/debt/<workflow-id-slug>-debt.md`.
4. Link related requirement, plan, task IDs, ADRs, and verification gaps.
5. Include close criteria.
6. Update `specs/index.md` notes when debt affects workflow completion or follow-up tracking.

## Output

- `docs/debt/<workflow-id-slug>-debt.md`
- optional updated `specs/index.md`
