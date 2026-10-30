# Debt Stage

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

1. Use `templates/debt-template.md`.
2. Create or update `docs/debt/<workflow-id-slug>-debt.md`.
3. Link related requirement, plan, task IDs, ADRs, and verification gaps.
4. Include close criteria.

## Output

- `docs/debt/<workflow-id-slug>-debt.md`
