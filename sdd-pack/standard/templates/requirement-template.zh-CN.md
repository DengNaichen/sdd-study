---
requirement_id: REQ-AREA-NAME
title: "[能力/模块名称]"
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

# Requirement: [能力/模块名称]

## 1. File Category *(必填)*

<!--
  需要操作：本节用于定义这个文件的类别。
  Requirement 是长期需求资产，不是一次变更的 spec、plan 或 tasks。
-->

| Dimension | Value | Meaning |
|---|---|---|
| Scope | [product / system / change / release / execution] | 它描述哪个范围 |
| Information Type | requirements | 它承载长期需求事实 |
| Authority | authoritative | 它是这些需求事实的权威来源 |
| Lifecycle | living | 它需要随产品/系统变化长期维护 |

## 2. Purpose & Scope *(必填)*

<!--
  需要操作：说明这个 Requirement 覆盖什么、不覆盖什么。
  只写长期有效的需求边界，不写执行计划。
-->

### Purpose

[说明这个能力为什么存在，以及它解决什么长期问题。]

### In Scope

- [本 Requirement 覆盖的能力、场景或规则]

### Out of Scope

- [本 Requirement 明确不覆盖的内容]

## 3. Requirements *(必填)*

<!--
  需要操作：记录长期有效、可开发、可测试的需求事实。
  不要求在模板里展开每个字段；需要时再在具体 Requirement 中补充。
-->

### User Stories & Priorities

<!--
  需要操作：记录可被 plan.md 和 tasks.md 消费的用户故事。
  每个故事必须有稳定 ID、优先级和独立验证方式。
-->

- **US1 (P1)**：[作为某类用户]，我想要 [能力]，以便 [价值]。
  - **Independent Test**：[如何不依赖其他故事验证该故事]
- **US2 (P2)**：[作为某类用户]，我想要 [能力]，以便 [价值]。
  - **Independent Test**：[如何不依赖其他故事验证该故事]

### Functional Requirements

- **FR-001**：系统必须 [长期有效的系统行为]
- **FR-002**：用户必须能够 [长期有效的用户能力]

*标记 unclear requirement 的示例：*

- **FR-003**：[需要澄清：未定义触发条件、完成标准或适用范围]

### Business Rules & Constraints

- **BR-001**：[长期有效的业务规则或约束]

### Non-Functional Requirements

- **NFR-001**：[性能、安全、隐私、可靠性、可观测性或兼容性要求]

### Data & Interfaces

- [关键数据、状态、接口或外部依赖；没有则写“无新增数据或接口需求”。]

## 4. Acceptance Criteria *(必填)*

<!--
  需要操作：用可测试语言描述完成标准。
-->

- **AC-001**：**Given** [初始状态]，**When** [操作或触发条件]，**Then** [可观察结果]
- **AC-002**：**Given** [边界或异常状态]，**When** [操作或触发条件]，**Then** [预期处理结果]

## 5. Assumptions & Open Questions *(必填)*

<!--
  需要操作：记录默认假设和仍需确认的问题。
-->

### Assumptions

- [当前采用的默认假设]

### Open Questions

- [需要进一步确认的问题]

## 6. Traceability & Change Log *(必填)*

<!--
  需要操作：记录来源、关联资产和变更历史。
  过期内容应标记 Deprecated 或 Superseded，不要无痕删除。
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
    change: "[变更摘要]"
    reason: "[变更原因]"
```
