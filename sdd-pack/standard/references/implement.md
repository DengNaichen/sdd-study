# Implement Stage

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

1. Resolve the active workflow from `specs/index.md`.
2. Select scope:
   - empty user request: next unchecked task
   - `all`: all unchecked tasks in dependency order
   - phase/story/task ID: selected scope only
2. Review the selected task(s) for blockers:
   - contradictions with requirement/plan/ADR
   - missing Files/Interfaces/TDD steps
   - missing dependencies
3. Execute each task.
4. Run task review before checking it off:
   - changed files match Files block
   - produced interfaces match Interfaces block
   - relevant acceptance criteria are covered
   - verification output is fresh
5. Run phase Review Gate after completing a phase.
6. Run debt capture check after selected scope completes.

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
