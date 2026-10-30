---
name: standard-sdd-implement
description: Use when executing Standard SDD tasks.md, continuing implementation, selecting unchecked tasks, applying TDD, performing task review, running Review Gates, and capturing accepted debt after implementation.
---

# Standard SDD Implement

Goal: execute `tasks.md` using Spec Kit-style artifacts and Superpowers-style execution discipline.

## Inputs

- `<workflow_directory>/requirement.md`
- `<workflow_directory>/plan.md`
- `<workflow_directory>/tasks.md`
- relevant ADRs
- relevant accepted debt

## Execution Discipline

- Review selected task scope before editing.
- Follow task steps exactly.
- Use TDD for behavior changes:
  - write failing test
  - verify expected failure
  - implement minimal code
  - verify pass
  - refactor only after green
- If a verification fails unexpectedly, find root cause before fixing.
- Do not mark tasks complete based on assumptions.
- Do not claim completion without fresh verification evidence.

## Process

1. Resolve the active workflow using `../workflow/SKILL.md` rules.
2. Read `specs/index.md`, `<workflow_directory>/requirement.md`, `<workflow_directory>/plan.md`, and `<workflow_directory>/tasks.md`.
3. Select scope:
   - empty user request: next unchecked task
   - `all`: all unchecked tasks in dependency order
   - phase/story/task ID: selected scope only
4. Review the selected task(s) for blockers:
   - contradictions with requirement/plan/ADR
   - missing Files/Interfaces/TDD steps
   - missing dependencies
5. Execute each task.
6. Run task review before checking it off:
   - changed files match Files block
   - produced interfaces match Interfaces block
   - relevant acceptance criteria are covered
   - verification output is fresh
7. Run phase Review Gate after completing a phase.
8. Update the workflow row in `specs/index.md` with stage `implement` or `review`, depending on remaining work.
9. Run debt capture check after selected scope completes. Use the Debt skill when accepted non-blocking follow-up work exists.
10. Move the workflow to `specs/complete/<id-slug>/` only after acceptance/review is complete, then update `specs/index.md` status/path/stage.

## Stop Conditions

Stop and report instead of guessing when:

- task is underspecified
- dependency is missing
- verification fails repeatedly
- plan and task contradict each other
- fixing would require redesigning the feature

## Output

- updated code
- updated `tasks.md` checkboxes
- updated `specs/index.md`
- verification results
- Review Gate status
- optional `docs/debt/<workflow-id-slug>-debt.md`
