---
name: standard-sdd-adr
description: Use when recording one durable Standard SDD architecture or design decision as an ADR, especially after plan.md or research.md identifies a long-lived tradeoff that future maintainers need to understand.
---

# Standard SDD ADR

Goal: create `docs/adr/ADR-XXXX-kebab-title.md` for one durable decision and maintain `docs/adr/index.md`.

ADR is a filtered output from plan/research, not a copy of all research.

## Create ADR When

- Future maintainers will ask "why was this done?"
- The decision changes architecture, module boundaries, public interfaces, data model, deployment, runtime, or operational policy.
- A credible alternative was rejected.
- The tradeoff affects multiple features or future implementation plans.
- The decision should outlive the current feature.

## Do Not Create ADR For

- Local implementation details.
- One-off workarounds.
- Library usage notes.
- Research findings fully consumed by the current plan.
- Choices obvious from code or project conventions.

## Process

1. Identify exactly one decision.
2. Read `docs/adr/index.md` first; if it does not exist, create it from `templates/adr-index-template.md` or `templates/adr-index-template.zh-CN.md`.
3. Resolve the next ADR number from both `docs/adr/index.md` and `docs/adr/ADR-*.md`; if they disagree, trust the highest existing filesystem number.
4. Use `templates/adr-template.md` or `templates/adr-template.zh-CN.md`.
5. Make the title express both the problem and the selected option, for example `ADR-0002: Use event-driven sync for order status`.
6. Fill participant fields:
   - Decision makers: people or teams accountable for the outcome.
   - Consulted: people who provided input but do not own the final call.
   - Informed: people who need to know the decision.
7. Fill confidence:
   - High: supported by production experience, data, or strong constraints.
   - Medium: enough evidence to proceed, with known verifiable risk.
   - Low: requires PoC, experiment, or later review; reassessment triggers are mandatory.
8. End Context and Problem with a clear decision question when useful.
9. Rank Decision Drivers by importance; do not turn them into background notes.
10. Analyze only credible options that were actually considered; keep "status quo" only when it was viable.
11. Select exactly one option in Decision Outcome and explain why other options were rejected.
12. Make Validation executable; write `N/A` for categories that do not apply instead of leaving blanks.
13. Make Reassessment Triggers concrete, such as cost, scale, failure rate, team constraints, or external dependency changes.
14. Link related `requirement.md`, `plan.md`, `research.md`, contracts, issues, PRs, PoCs, benchmarks, or ADRs.
15. After creating or updating the ADR file, immediately update the matching row in `docs/adr/index.md`.

## Index Rules

- `docs/adr/index.md` is the ADR management entrypoint; do not read every ADR by default just to understand existing decisions.
- The index must list ADR number, date, status, decision summary, confidence, file link, supersession relation, and references.
- Add a row when creating an ADR.
- Update the row when ADR status changes.
- When one ADR supersedes another, update `Supersedes` and `Superseded by` for both affected rows.
- Keep the index decision summary to one sentence; do not copy ADR body content.

## Filling Rules

- Do not copy full research; extract only decision evidence.
- Do not put multiple independent decisions into one ADR.
- Follow-up work is only for non-blocking items; blocking implementation work belongs in plan/tasks.
- If status is `Superseded`, fill `Superseded by`.
- If this ADR replaces an earlier ADR, fill `Supersedes`.
- Keep the ADR short, durable, and explanatory.

## Output

- `docs/adr/index.md`
- `docs/adr/ADR-XXXX-kebab-title.md`
