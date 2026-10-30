---
requirement_id: REQ-AREA-NAME
title: "[Capability / module name]"
category: Requirement
scope_level: "[product / system / change / release / execution]"
information_type: requirements
authority: authoritative
lifecycle: living
status: Draft
owner: "[owner / team]"
created: YYYY-MM-DD
source:
  refs:
    - "[feature spec / PRD / issue / customer feedback / decision]"
---

# Requirement: [Capability / module name]

## 1. File Category *(required)*

<!--
  Action needed: define what kind of file this is.
  Requirement is a long-lived requirement asset, not a one-off spec, plan, or task list.
-->

| Dimension | Value | Meaning |
|---|---|---|
| Scope | [product / system / change / release / execution] | Which scope this file describes |
| Information Type | requirements | It carries long-lived requirement facts |
| Authority | authoritative | It is the source of truth for these requirement facts |
| Lifecycle | living | It must be maintained as the product/system changes |

## 2. Purpose & Scope *(required)*

<!--
  Action needed: explain what this Requirement covers and does not cover.
  Record durable requirement boundaries, not execution plans.
-->

### Purpose

[Explain why this capability exists and what long-lived problem it solves.]

### In Scope

- [Capabilities, scenarios, or rules covered by this Requirement]

### Out of Scope

- [Content explicitly not covered by this Requirement]

## 3. Requirements *(required)*

<!--
  Action needed: record durable, buildable, testable requirement facts.
  Expand sections only as needed for the concrete Requirement.
-->

### User Stories & Priorities

<!--
  Action needed: record user stories that plan.md and tasks.md can consume.
  Each story needs a stable ID, priority, and independent verification method.
-->

- **US1 (P1)**: As a [user type], I want [capability], so that [value].
  - **Independent Test**: [How to verify this story without depending on other stories]
- **US2 (P2)**: As a [user type], I want [capability], so that [value].
  - **Independent Test**: [How to verify this story without depending on other stories]

### Functional Requirements

- **FR-001**: The system must [durable system behavior]
- **FR-002**: Users must be able to [durable user capability]

*Example unclear requirement marker:*

- **FR-003**: [NEEDS CLARIFICATION: undefined trigger condition, completion standard, or scope]

### Business Rules & Constraints

- **BR-001**: [Durable business rule or constraint]

### Non-Functional Requirements

- **NFR-001**: [Performance, security, privacy, reliability, observability, or compatibility requirement]

### Data & Interfaces

- [Key data, state, interface, or external dependency; if none, write "No new data or interface requirements."]

## 4. Acceptance Criteria *(required)*

<!--
  Action needed: describe completion standards in testable language.
-->

- **AC-001**: **Given** [initial state], **When** [operation or trigger], **Then** [observable result]
- **AC-002**: **Given** [boundary or error state], **When** [operation or trigger], **Then** [expected handling]

## 5. Assumptions & Open Questions *(required)*

<!--
  Action needed: record default assumptions and questions that still need confirmation.
-->

### Assumptions

- [Current default assumption]

### Open Questions

- [Question that needs further confirmation]

## 6. Traceability & Change Log *(required)*

<!--
  Action needed: record sources, related assets, and change history.
  Mark stale content as Deprecated or Superseded instead of silently deleting it.
-->

```yaml
traceability:
  sources:
    - "[feature spec / PRD / issue / ADR / PR / customer feedback]"
  links:
    specs: []
    adrs: []
    issues: []
    prs: []
    tests: []

change_log:
  - date: YYYY-MM-DD
    version: "0.1"
    change: "[change summary]"
    reason: "[reason]"
```
