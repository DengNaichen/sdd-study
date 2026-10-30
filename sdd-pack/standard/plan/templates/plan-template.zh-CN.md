# 实施计划：[功能名称]

**分支**：`[###-feature-name]` | **日期**：[DATE] | **Requirement**：[链接]

**输入**：来自 `/specs/[###-feature-name]/requirement.md` 或链接的 Requirement 源的需求

**注意**：此模板由 Standard SDD 的 Plan 阶段填充。

## 概要

[从 Requirement 中提取：主要需求、范围和选定的技术方案。仅在需要研究时包含研究决策。]

## 范围检查 (Scope Check)

<!--
  如果 Requirement 覆盖多个独立的子系统，每个子系统都应该有自己的计划。
  每个计划都应该能够产出独立工作、独立测试的软件。
  如果是单一系统，写上 "单一系统 —— 无需拆分" 并继续。
-->

[单一系统 —— 无需拆分 | 拆分为：plan-A.md, plan-B.md, ...]

## 技术上下文 (Technical Context)

<!--
  需要操作：用项目的具体技术细节替换此部分内容。
  此处的结构仅为建议性，用于引导迭代过程。
-->

**语言/版本**：[例如，Python 3.11, Swift 5.9, Rust 1.75 或 需澄清]

**主要依赖**：[例如，FastAPI, UIKit, LLVM 或 需澄清]

**存储**：[如果适用，例如，PostgreSQL, CoreData, 文件 或 不适用]

**测试**：[例如，pytest, XCTest, cargo test 或 需澄清]

**目标平台**：[例如，Linux 服务器, iOS 15+, WASM 或 需澄清]

**项目类型**：[例如，library/cli/web-service/mobile-app/compiler/desktop-app 或 需澄清]

**性能目标**：[领域特定，例如，1000 req/s, 10k lines/sec, 60 fps 或 需澄清]

**约束条件**：[领域特定，例如，<200ms p95, <100MB memory, offline-capable 或 需澄清]

**规模/范围**：[领域特定，例如，10k 用户, 1M LOC, 50 页面 或 需澄清]

## 测试策略 (Test Strategy)

<!--
  需要操作：定义如何证明此项变更是正确的。
  保持这部分为策略性说明，而不是具体任务清单。具体的 红/绿 (Red/Green) 步骤属于 tasks.md。
-->

**测试框架**：[例如，pytest, XCTest, cargo test, Playwright 或 需澄清]

**测试先行范围 (Test-First Scope)**：[应从编写失败测试开始的行为，或说明不适用的原因]

**契约测试 (Contract Tests)**：[需首先测试的外部 API/事件/CLI/库契约，或不适用]

**集成测试 (Integration Tests)**：[端到端或跨组件流，或不适用]

**单元/回归测试 (Unit/Regression Tests)**：[核心逻辑、边界情况、Bug 回归，或不适用]

**手动验证 (Manual Verification)**：[仍有必要的手动/浏览器/设备验证，或不适用]

**需要红/绿证据**：[是/否；如果为"是"，tasks.md 必须要求在实现前输出失败结果，并在实现后输出通过结果]

## 宪法检查 (Constitution Check)

*门禁 (GATE)：必须在阶段 0 (Phase 0) 研究之前通过。在阶段 1 (Phase 1) 设计之后重新检查。*

[基于项目宪法文件确定的门禁条件]

## 辅助工件 (Supporting Artifacts)

<!--
  计划 (Plan) 是必需的设计工件。
  研究 (Research) 和契约 (Contracts) 是可选的辅助材料。
  数据模型文档默认不生成；如果项目已有现有的数据模型源，请进行引用。
-->

| 工件 | 必须？ | 策略说明 |
|----------|-----------|--------|
| `plan.md` | 是 | 此变更的实现策略与技术设计 |
| `research.md` | 可选 | 仅在有未决决策、技术选择、外部约束或风险验证时创建 |
| `contracts/` | 可选 | 针对 API/事件/CLI/库契约创建；后续可归档到正式的契约目录中 |
| `data-model.md` | 否 | 默认不生成；在相关时链接到项目专属的数据模型文档 |
| `tasks.md` | 后续 | 由 Tasks 阶段生成；每个任务都带有 Files/Interfaces 声明和 TDD 微步骤 |

## 文件结构映射 (File Structure Mapping)

<!--
  需要操作：在生成 tasks.md 之前，规划出将要创建或修改哪些文件以及每个文件负责什么。
  此映射将直接驱动 tasks.md 中每个 Task 的 Files 和 Interfaces 声明。

  设计具有清晰边界和明确定义接口的单元。
  每个文件应该有且仅有一项清晰的职责。
  共同变化的文件应该放在一起 —— 按职责拆分，而不是按技术层拆分。
  在现有代码库中，请遵循已有的设计模式。
-->

| 操作 (Operation) | 文件路径 (File Path) | 职责 (Responsibility) | 故事 (Story) |
|-----------|-----------|----------------|-------|
| Create | `src/models/[entity].py` | [Entity] 定义与仓储 (repository) | [US1] |
| Create | `src/services/[service].py` | [Service] 业务逻辑 | [US1] |
| Modify | `src/api/routes.py:45-60` | 添加 [resource] 路由 | [US1] |
| Create | `tests/unit/test_[entity].py` | [Entity] 模型单测 | [US1] |
| Create | `tests/integration/test_[endpoint].py` | [Endpoint] 集成测试 | [US1] |

## 项目结构 (Project Structure)

### 文档结构（当前功能）

```text
specs/[###-feature]/
├── requirement.md               # 本功能的需求输入
├── plan.md              # 本文件（Plan 阶段输出）
├── research.md          # 可选：需要研究时的决策依据
├── contracts/           # 可选：需要时的外部接口契约
└── tasks.md             # Tasks 阶段输出 —— 非 Plan 阶段创建
```

### 源代码（仓库根目录）
<!--
  需要操作：用此功能的具体布局替换下面的占位目录树。
  删除未使用的选项，并用真实路径扩展所选结构（例如，apps/admin, packages/something）。
  交付的计划中不得包含 Option 标签。
-->

```text
# [若未使用则删除] 选项 1：单项目结构（默认）
src/
├── models/
├── services/
├── cli/
└── lib/

tests/
├── contract/
├── integration/
└── unit/

# [若未使用则删除] 选项 2：Web 应用结构（当检测到 "frontend" + "backend" 时）
backend/
├── src/
│   ├── models/
│   ├── services/
│   └── api/
└── tests/

frontend/
├── src/
│   ├── components/
│   ├── pages/
│   └── services/
└── tests/

# [若未使用则删除] 选项 3：移动端 + API（当检测到 "iOS/Android" 时）
api/
└── [与上方 backend 相同]

ios/ 或 android/
└── [平台特定结构：功能模块、UI 流、平台测试]
```

**结构决策**：[记录选定的结构并引用上方确定的具体实际目录]

## 复杂度跟踪 (Complexity Tracking)

> **仅在 Constitution Check 出现不合规项且必须给出合理解释时填写**

| 违规项 | 为什么需要 | 拒绝更简单替代方案的原因 |
|-----------|------------|-------------------------------------|
| [例如，第 4 个项目] | [当前需求] | [为什么 3 个项目不够用] |
| [例如，Repository 模式] | [具体问题] | [为什么直接访问数据库不够用] |
