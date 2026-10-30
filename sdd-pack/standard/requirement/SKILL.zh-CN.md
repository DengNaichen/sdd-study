---
name: standard-sdd-requirement
description: 当需要为 Standard SDD 功能定义、澄清、创建或更新权威 requirement.md 时使用，包括用户故事、功能需求、验收标准、假设和追踪关系。
---

# Standard SDD Requirement

目标：创建或更新 `<workflow_directory>/requirement.md`。

当用户希望定义功能、澄清行为或建立长期需求来源时使用。

## 输入

- 用户请求、PRD、issue、已有笔记或当前功能上下文。
- 更新时读取已有 `<workflow_directory>/requirement.md`。

## Workflow 解析

- 使用 `../workflow/SKILL.zh-CN.md` 规则。
- 新 requirement 默认进入 `specs/active/<id-slug>/`。
- 创建新 workflow 前先读取或创建 `specs/index.md`。
- 更新时根据用户给出的 ID、slug、路径或明确上下文选择 workflow。

## 流程

1. 确定功能目录：
   - 如果工作区中明显存在当前功能，优先使用已有目录。
   - 否则根据下一个 ID 和能力名称选择 `specs/active/<id-slug>/`。
2. 必要时创建目录。
3. 在 `specs/index.md` 中新增或更新 workflow 行。
4. 中文 artifact 使用 `templates/requirement-template.zh-CN.md`；英文 artifact 使用 `templates/requirement-template.md`。
5. 填充长期需求内容：
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
6. 除非需求身份发生变化，否则保留已有 requirement ID。

## 规则

- Requirement 不是实现计划、任务清单、PR 摘要或对话记录。
- 优先采用合理默认值，并记录到 Assumptions。
- 只有当歧义会改变长期产品/系统行为时，才使用 `[NEEDS CLARIFICATION: ...]`。
- 澄清标记最多 3 个。

## 输出

- `<workflow_directory>/requirement.md`
- 更新后的 `specs/index.md`
- 报告是否已经准备好进入 Plan 阶段。
