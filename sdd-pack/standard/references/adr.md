# ADR Stage

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
2. Read `docs/adr/index.md` first; if it does not exist, create it from `templates/adr-index-template.md`.
3. Resolve the next ADR number from both `docs/adr/index.md` and `docs/adr/ADR-*.md`.
4. Use `templates/adr-template.md`.
5. Make the title express both the problem and the selected option.
6. Fill decision makers, consulted, informed, and confidence.
7. End context with a clear decision question.
8. Rank decision drivers by importance.
9. Analyze only credible options that were actually considered.
10. Select exactly one option in the decision outcome and explain why.
11. Define validation and reassessment triggers.
12. Link related `requirement.md`, `plan.md`, `research.md`, contracts, issues, PRs, PoCs, benchmarks, or ADRs.
13. After creating or updating the ADR file, update `docs/adr/index.md`.
14. Keep the ADR short and durable.

## Index Rules

- `docs/adr/index.md` is the ADR management entrypoint; do not read every ADR by default just to understand existing decisions.
- The index must list ADR number, date, status, decision summary, confidence, file link, supersession relation, and references.
- Update the index whenever ADR status or supersession relation changes.

## Filling Rules

- Do not copy full research; extract only decision evidence.
- Do not put multiple independent decisions into one ADR.
- Follow-up work is only for non-blocking items; blocking implementation work belongs in plan/tasks.
- If status is `Superseded`, fill `Superseded by`.
- If this ADR replaces an earlier ADR, fill `Supersedes`.

## Output

- `docs/adr/index.md`
- `docs/adr/ADR-XXXX-kebab-title.md`
