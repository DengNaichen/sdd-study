---
name: standard-sdd-tasks
description: Use after requirement.md and plan.md exist to generate Standard SDD tasks.md with user-story phases, Files blocks, Interfaces blocks, TDD micro-steps, dependencies, and Review Gates.
---

# Standard SDD Tasks

Goal: create `<workflow_directory>/tasks.md` from `requirement.md` and `plan.md`.

Use this stage after `plan.md` exists and File Structure Mapping is complete.

## Inputs

- `<workflow_directory>/requirement.md`
- `<workflow_directory>/plan.md`
- optional `research.md`
- optional `contracts/`
- optional existing ADRs referenced by plan

## Process

1. Resolve the active workflow using `../workflow/SKILL.md` rules.
2. Read `specs/index.md`, `<workflow_directory>/requirement.md`, and `<workflow_directory>/plan.md`.
3. Use `templates/tasks-template.md` or `templates/tasks-template.zh-CN.md`.
4. Extract user stories and priorities from `requirement.md`.
5. Extract technical context and File Structure Mapping from `plan.md`.
6. Map contracts and decisions to the stories they affect.
7. Generate phases:
   - Phase 1: Setup
   - Phase 2: Foundational
   - Phase 3+: one phase per user story, in priority order
   - Final Phase: Polish & Cross-Cutting Concerns
8. Each standard task must include:
   - H3 task header with sequential ID
   - `[P]` only when parallelizable
   - `[US#]` for user story tasks
   - Files block
   - Interfaces block
   - TDD micro-steps
9. Each phase must end with a Review Gate.
10. Update the workflow row in `specs/index.md` with stage `tasks` and current updated date.

## Prohibited Patterns

- TBD/TODO/fill in later
- vague "add validation" or "handle errors"
- missing file paths
- missing concrete test/verification steps
- interfaces that reference undefined types or functions

## Output

- `<workflow_directory>/tasks.md`
- updated `specs/index.md`
- Summary of task count, story breakdown, parallel opportunities, and MVP scope
