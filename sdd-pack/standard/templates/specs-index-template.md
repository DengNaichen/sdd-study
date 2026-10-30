# Specs Index

This file is the Standard SDD workflow registry. Read it before choosing, creating, or completing a workflow.

## Workflows

| ID | Status | Feature | Path | Stage | Created | Updated | Notes |
|---|---|---|---|---|---|---|---|
| 0000 | complete | Example completed workflow | specs/complete/0000-example-done | complete | YYYY-MM-DD | YYYY-MM-DD | Example row; remove when real workflows exist |

## Status

- active: work is currently in progress.
- blocked: work cannot continue without input or external change.
- complete: work has passed acceptance/review and moved to `specs/complete/`.

## Stage

- requirement
- plan
- adr-check
- tasks
- implement
- review
- complete

## Maintenance Rules

- Create one row per workflow directory.
- Keep `Path` in sync when moving from `specs/active/` to `specs/complete/`.
- Update `Stage` whenever the workflow advances.
- Update `Updated` whenever any workflow artifact changes.
- Do not copy requirement, plan, tasks, or ADR body content into this index.
