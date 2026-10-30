# Requirement Stage

Goal: create or update `<workflow_directory>/requirement.md`.

Use when the user wants to define a feature, clarify behavior, or establish the long-lived requirement source.

## Inputs

- User request, PRD, issue, existing notes, or current feature context.
- Existing `<workflow_directory>/requirement.md` when updating.

## Process

1. Resolve the feature directory:
   - Prefer an existing active feature if obvious from the workspace.
   - Otherwise choose `specs/active/<id-slug>/` from the next ID and capability name.
2. Create the directory if needed.
3. Add or update the workflow row in `specs/index.md`.
4. Use `templates/requirement-template.zh-CN.md`.
5. Fill durable requirement content:
   - File Category
   - Purpose & Scope
   - User Stories & Priorities
   - Functional Requirements
   - Business Rules & Constraints
   - Non-Functional Requirements
   - Data & Interfaces
   - Acceptance Criteria
   - Assumptions & Open Questions
   - Traceability & Change Log
6. Preserve existing requirement IDs unless the requirement identity changed.

## Rules

- Requirement is not a plan, task list, PR summary, or conversation transcript.
- Prefer reasonable defaults and record them in Assumptions.
- Use `[NEEDS CLARIFICATION: ...]` only when ambiguity changes long-lived product/system behavior.
- Limit clarification markers to 3.

## Output

- `<workflow_directory>/requirement.md`
- updated `specs/index.md`
- Report whether it is ready for planning.
