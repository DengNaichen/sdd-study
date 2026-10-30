---
name: standard-sdd-plan
description: Use after requirement.md exists to create or update plan.md, technical context, file structure mapping, test strategy, optional research.md, optional contracts, and ADR recommendations for Standard SDD.
---

# Standard SDD Plan

Goal: create or update `<workflow_directory>/plan.md`, with optional `research.md` and `contracts/`.

Use this stage after `requirement.md` exists.

## Inputs

- `<workflow_directory>/requirement.md`
- Existing project structure and conventions
- Relevant architecture docs, ADRs, contracts, or source files

## Process

1. Resolve the active workflow using `../workflow/SKILL.md` rules.
2. Read `specs/index.md` and `<workflow_directory>/requirement.md`.
3. Use `templates/plan-template.md` or `templates/plan-template.zh-CN.md`.
4. Fill Technical Context from the actual project.
5. Fill Test Strategy:
   - framework
   - test-first scope
   - contract/integration/unit/manual verification
   - whether Red/Green evidence is required in tasks
6. Fill File Structure Mapping before tasks are generated.
7. Generate `research.md` only when real uncertainty exists:
   - unresolved decisions
   - technology choices
   - external constraints
   - contract exploration
   - meaningful risk validation
8. Generate `contracts/` only when there are public APIs, events, CLI contracts, library contracts, UI contracts, or other external interfaces.
9. Do not generate `data-model.md` by default; link existing project-owned data model docs when relevant.
10. Update the workflow row in `specs/index.md` with stage `plan` and current updated date.

## ADR Recommendation Check

After planning, recommend ADR only when plan/research contains a durable decision:

- architecture or module boundary changes
- public interface, contract, event, or CLI choices
- data model, schema, deployment, runtime, or operational policy decisions
- rejection of another credible option
- tradeoffs likely to affect multiple features

Do not create ADR automatically.

## Output

- `<workflow_directory>/plan.md`
- optional `<workflow_directory>/research.md`
- optional `<workflow_directory>/contracts/`
- updated `specs/index.md`
- recommendation for ADR only when warranted
