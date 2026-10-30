---
description: Legacy command wrapper for the Standard SDD Implement stage.
---

# Implement

This command file is retained for compatibility/reference. The canonical workflow lives in `standard/SKILL.md` and `standard/implement/SKILL.md`.

## User Input

```text
$ARGUMENTS
```

Execute selected unchecked tasks from:

```text
specs/active/<id-slug>/tasks.md
```

Update `specs/index.md` during implementation. Move to `specs/complete/<id-slug>/` only after acceptance/review is done.

Use:

- `requirement.md` for expected behavior and acceptance criteria
- `plan.md` for design constraints and verification strategy
- relevant ADRs for durable design constraints

Execution discipline:

- review selected scope before editing
- follow task steps exactly
- use TDD for behavior changes
- debug root cause before fixing unexpected failures
- run task review before marking complete
- run phase Review Gate when phase completes
- verify before claiming completion
- capture accepted non-blocking debt after implementation
