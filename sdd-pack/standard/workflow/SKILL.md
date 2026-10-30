---
name: standard-sdd-workflow
description: Use when managing Standard SDD workflow registry and feature directories: create numbered specs/active workflows, select an active workflow, update specs/index.md stage/status metadata, or move completed workflows to specs/complete.
---

# Standard SDD Workflow

Goal: manage numbered workflow directories and `specs/index.md` without loading every feature artifact.

## Layout

Use this structure:

```text
specs/
├── index.md
├── active/
│   └── 0001-feature-slug/
│       ├── requirement.md
│       ├── plan.md
│       ├── research.md      # optional
│       ├── contracts/       # optional
│       └── tasks.md
└── complete/
    └── 0000-example-done/
```

## Registry

`specs/index.md` is the workflow registry. Read it before selecting, creating, or completing a workflow.

If `specs/index.md` does not exist, create it from `templates/specs-index-template.md` or `templates/specs-index-template.zh-CN.md`.

The registry must track:

- ID
- status
- feature
- path
- current stage
- created date
- updated date
- notes

## Directory Rules

- Use `NNNN-kebab-slug`, for example `0007-billing-webhook`.
- Next ID is one greater than the largest ID found in `specs/index.md`, `specs/active/`, or `specs/complete/`.
- New workflows start in `specs/active/<id-slug>/`.
- Completed workflows move to `specs/complete/<id-slug>/`.
- Do not reuse IDs.
- Do not silently rename a workflow directory after artifacts exist; update `specs/index.md` if a rename is explicitly requested.

## Selection Rules

When a stage needs a feature directory:

1. If the user names an ID, slug, or path, use that workflow.
2. Else, read `specs/index.md` and match by current context.
3. Else, if exactly one active workflow exists, use it.
4. Else, if no active workflow exists and the user is starting a feature, create a new active workflow.
5. Else, ask the user to choose; do not guess among multiple active workflows.

## Stage Rules

- Requirement creation creates a new active workflow unless the user clearly updates an existing one.
- Plan, Tasks, and Implement require an active workflow unless the user explicitly targets a completed workflow for review/update.
- Completing implementation does not automatically move a workflow to `complete`; move it only when acceptance/review is done.
- When moving to `complete`, update status, path, stage, and updated date in `specs/index.md`.

## Output

- selected or created workflow path
- registry row updated
- next recommended stage
