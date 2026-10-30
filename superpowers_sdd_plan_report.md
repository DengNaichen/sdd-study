# Superpowers 对 SDD Plan 目标态的借鉴报告

## 结论

Superpowers 的目标形态值得借鉴，但要拆开学：

- 借鉴它的 `plan` 可执行性：精确文件、接口、步骤、验证命令、期望输出、任务级 review。
- 不照搬它把 task 明细直接塞满 plan 的重量级做法。
- 我们的 SDD 目标态应明确：`spec/plan/tasks` 是轻量执行介质，真正长期沉淀的是架构、关键决策、接口契约和领域模型。

推荐的 `plan.md` 不是 current design snapshot，而是：

```text
Current State -> Target State -> Gap -> Approach -> Risks -> Validation -> Task Seeds
```

其中 `Task Seeds` 只给足生成 `tasks.md` 所需的信息，不必像 Superpowers 一样在 plan 中写完整代码级步骤。

## 更新后的共识：执行过程轻量，用完即丢

这次 SDD 流程设计的核心边界应改成：

- `spec` 可以存在，但它主要是对齐意图和验收标准的工作介质，不必被神化成永久真理。
- 中间执行过程要轻量：`plan.md`、`tasks.md`、agent brief、report、review package 都应默认是一次性执行痕迹。
- 长期资产应是架构、关键决策、接口契约、领域模型、已验证的不变量和重要取舍。
- 流程的价值不是生产更多文档，而是把一次变更中值得保留的判断沉淀到正确位置。

因此目标态不是“SpecKit 生成一整套永久文档”，而是：

```text
Intent alignment -> lightweight execution -> verified change -> durable knowledge capture
```

执行结束后，应主动判断哪些内容需要流回长期资产：

- 架构变化 -> `design.md` 或 ADR
- 关键取舍 -> decision record
- 接口变化 -> `contracts/`
- 领域概念变化 -> `data-model.md`
- 用户目标或验收变化 -> `spec.md`
- 纯执行步骤 -> 丢弃或保留为历史 trace，不作为长期 source of truth

## Superpowers 的实际分工

Superpowers 已经有清晰的分层：

- `docs/superpowers/specs/*-design.md`：设计/决策文档。由 brainstorming 生成，用户 review 后才进入 plan。参考 `superpowers/skills/brainstorming/SKILL.md:20-33`、`:102-131`。
- `docs/superpowers/plans/*.md`：执行计划。由 writing-plans 生成，面向 agent/engineer 执行。参考 `superpowers/skills/writing-plans/SKILL.md:18`、`:54-79`。
- `.superpowers/sdd/*`：执行期 scratch，包括 task brief、report、review package、progress ledger。参考 `superpowers/skills/subagent-driven-development/SKILL.md:219-264`。
- `skills/*/SKILL.md`：长期行为规范，基本等同“会影响 agent 行为的代码”。

这个分工支持我们的判断：`plan.md` 不应承载“当前设计事实快照”，而应承载“这次变更怎么落地”。

## Superpowers Plan 最值得借鉴的点

### 1. Plan 是执行入口，不是设计百科

Superpowers 的 plan 头部非常短：

- `Goal`
- `Architecture`
- `Tech Stack`
- `Global Constraints`

参考 `superpowers/skills/writing-plans/SKILL.md:54-77`。

这适合 SDD：plan 应把执行者需要的约束提出来，而不是要求执行者反复跨 `spec/design/research` 猜上下文。

### 2. Global Constraints 很关键

Superpowers 把版本、依赖、命名、平台等硬约束复制到 plan 头部。参考 `superpowers/skills/writing-plans/SKILL.md:69-74`。

这点应直接采用。原因：后续生成 task brief、review prompt、validation checklist 时，可以机械提取这些约束，减少遗漏。

### 3. File Map 比通用 Project Structure 更实用

Superpowers 的实际 plan 会列出本次变更要改哪些文件、每个文件承担什么职责。参考 `superpowers/docs/superpowers/plans/2026-06-10-visual-companion-auth-hardening.md:15-40`。

这比“单项目/web/mobile 三选一”的模板树更适合 future implementation plan。

建议目标态使用：

```md
## File Map

- Modify: `path/to/file`
  - Why this file changes
  - Responsibility after change
- Create: `path/to/new-file`
  - Responsibility
  - Consumers
```

### 4. 每个任务要有 Interfaces

Superpowers 要求每个 task 写：

- `Consumes`
- `Produces`
- 精确函数名、参数、返回类型

参考 `superpowers/skills/writing-plans/SKILL.md:89-94`。

这非常适合 agentic SDD，因为 task 常被拆给不同 agent。接口写清楚，才能避免跨 task 名称漂移、重复实现、隐式耦合。

### 5. Task 必须可独立 review

Superpowers 的 task right-sizing 标准是：一个 task 是最小的、带自己测试循环的、值得单独 reviewer gate 的单元。参考 `superpowers/skills/writing-plans/SKILL.md:36-43`。

建议纳入目标态：`tasks.md` 的任务不应只是“改某文件”，而应是一个可验证增量。

### 6. 验证命令要带 expected output

Superpowers plan 强调每步有命令和预期结果。参考 `superpowers/skills/writing-plans/SKILL.md:95-125`、`:138-142`。

这点应进入 SDD 的 `plan.md` 或 `tasks.md`，至少 `plan.md` 应定义 validation strategy，`tasks.md` 再展开为具体命令。

### 7. Plan 自审是必要 gate

Superpowers 要求 plan 自审：

- spec coverage
- placeholder scan
- type consistency

参考 `superpowers/skills/writing-plans/SKILL.md:144-154`。

建议目标态保留为 `Plan Readiness Check`，作为生成 `tasks.md` 前的 gate。

## 不应照搬的点

### 1. 不要让 plan 变成超长执行脚本

Superpowers 的 plan 常直接包含完整代码片段、每步命令、commit 指令。执行性极强，但对通用 SDD 来说可能过重。

更合理的分层：

- `plan.md`：当前状态、目标状态、差异、策略、风险、验证、任务种子。
- `tasks.md`：具体 task、路径、命令、预期输出、并行关系。

### 2. 不要把 Problem / Threat Model / Current Failures 塞进 plan 主体

Superpowers 的 design spec 会记录 problem、goals、non-goals、threat model、current failures。参考 `superpowers/docs/superpowers/specs/2026-06-09-sdd-task-scoped-review-dispatch-design.md:5-35`、`superpowers/docs/superpowers/specs/2026-06-10-visual-companion-auth-hardening-design.md:20-68`。

这些属于 `design.md` 或 `spec.md`。`plan.md` 可以引用和摘要，但不应变成设计记录。

### 3. 不要强制 subagent-per-task

Superpowers 的 SDD 核心是 fresh subagent per task + task review + final review。参考 `superpowers/skills/subagent-driven-development/SKILL.md:8-17`。

这适合 agent 工作流，但通用 SDD 应把它作为推荐执行模式，而不是文件结构本身的硬依赖。

### 4. 不要复制项目私有路径

`docs/superpowers/specs`、`docs/superpowers/plans` 是项目私有命名。通用 SDD 应使用中性路径：

```text
specs/[feature]/
  spec.md
  design.md
  plan.md
  tasks.md
  contracts/
  data-model.md
```

### 5. 不要把执行 scratch 当长期文档

Superpowers 的 `.superpowers/sdd/` 是恢复执行状态用的 scratch，不进 git。参考 `superpowers/skills/subagent-driven-development/SKILL.md:246-264`。

通用 SDD 也应区分：

- 长期：`design.md` / ADR、`contracts/`、`data-model.md`、关键不变量和决策记录
- 可保留：`spec.md`，仅保留仍有产品/验收价值的部分
- 一次性：`plan.md`、`tasks.md`
- scratch：agent briefs、reports、diff packages、progress ledger

## 推荐的 SDD 文档角色

| 文件 | 角色 | 生命周期 | Source of truth | 可否生成 tasks |
|---|---|---|---|---|
| `spec.md` | 用户目标、场景、需求、验收标准 | 可保留，但不必承载执行细节 | 用户意图和产品决策 | 间接 |
| `design.md` / ADR | 架构关系、关键取舍、限制、不变量 | 长期资产 | 代码、测试、已验证行为、设计决策 | 否 |
| `data-model.md` | 领域对象、状态、约束 | 长期资产 | 设计决策和数据契约 | 间接 |
| `contracts/` | 跨边界接口契约 | 长期资产 | 对外/跨模块 API | 间接 |
| `plan.md` | 一次 future change 的落地方案 | 一次性执行介质 | 目标行为 + 当前差异 + 变更决策 | 是 |
| `tasks.md` | 可执行任务清单 | 一次性执行介质 | `plan.md` | 执行输入 |
| agent briefs/reports | agent 执行交接和恢复 | scratch | `plan.md` / `tasks.md` | 否 |

## SpecKit 与 Superpowers 吸收对照

| SDD 模块 | 从 SpecKit 吸收 | 从 Superpowers 吸收 | 目标态取舍 |
|---|---|---|---|
| Feature 目录 | `specs/[feature]/` 的单 feature 工作区 | 日期命名的历史文档习惯 | 保留 SpecKit 的 feature 目录；日期可用于历史快照，不作为主结构 |
| `spec.md` | 用户故事、需求、验收标准、优先级 | brainstorming 的设计前置和用户 review gate | `spec.md` 做轻量 intent 对齐；只把有长期价值的验收变化沉淀下来 |
| `design.md` | 现有模板没有明确设计快照文件 | `*-design.md` 承载 problem、goals、non-goals、threat/current failures、design | 新增/强化 `design.md`，承载 current/target design snapshot |
| `data-model.md` | 独立数据模型产物 | 不突出为固定产物 | 保留 SpecKit 的独立数据模型，作为 design 的结构化补充 |
| `contracts/` | 独立接口契约目录 | task/reviewer 强依赖接口清晰 | 保留 SpecKit 的 contracts，并吸收 Superpowers 的 per-task Interfaces |
| `plan.md` | 作为 task generation 的上游 | future implementation plan，含 Goal、Architecture、Global Constraints、File Map | 重定义为 future plan，不再混 current design snapshot |
| Current/Target/Gap | 当前模板缺失 | 分散在 design/spec/issue catalog | 目标态把 `Current State / Target State / Gap` 固定进 `plan.md` |
| 约束 | Constitution Check、Technical Context | `Global Constraints` 可机械提取 | 治理留在 spec/design；执行硬约束复制进 `plan.md` |
| 文件结构 | 泛化 Project Structure 模板 | 本次变更 File Map | 用 File Map 替代泛化结构树 |
| Task 生成 | `tasks.md` 独立生成，按 user story 分组 | task right-sizing、每 task 可独立 review | `tasks.md` 从 `plan.md` 生成，同时保留 user story 映射 |
| Task 粒度 | checklist task，路径要求 | 每 task 有 Files、Interfaces、验证命令、expected output | `tasks.md` 承担细粒度步骤；`plan.md` 只放 task seeds |
| 测试策略 | tests optional，按 spec 请求生成 | TDD/RED-GREEN、focused test、full verification | 不强制 TDD，但每 task 必须有可验证标准 |
| Review gate | analyze/checklist/converge 等一致性命令 | spec review、plan review、task review、final review | 保留 SpecKit 的静态一致性检查，吸收 Superpowers 的执行 review gate |
| 执行恢复 | 当前模板层面不突出 | `.superpowers/sdd/progress.md` ledger、brief/report/review package | 引入 scratch execution state，但不进长期文档 |
| Extension/Hook | SpecKit hooks 可扩展 | Superpowers skill 流程强约束 | hooks 做机制；流程规则写入 SDD 文档/命令模板 |
| 长期文档 | spec/plan/tasks 都在 feature 目录 | dated artifacts 保留，scratch 忽略 | 长期只沉淀架构、关键决策、contracts、data-model；plan/tasks 是变更痕迹 |

## 推荐的 `plan.md` 目标模板

```md
# Implementation Plan: [FEATURE]

**Spec**: `spec.md`
**Design**: `design.md`
**Date**: [DATE]

## Goal

[One sentence: what this change delivers.]

## Current State

[What exists now. Link to design/code/tests when relevant.]

## Target State

[What must be true after this change.]

## Gap

[Concrete differences between current and target state.]

## Approach

[How we will close the gap. Key technical decisions only.]

## Global Constraints

- [Version floors, dependency limits, platform constraints]
- [Naming/copy/security/performance constraints]
- [Compatibility and migration constraints]

## File Map

- Create: `path`
  - Responsibility:
  - Consumed by:
- Modify: `path`
  - Change:
  - Reason:

## Interfaces

- Produces:
  - `[name/signature/schema]`
- Consumes:
  - `[name/signature/schema]`

## Risks And Mitigations

| Risk | Mitigation | Validation |
|---|---|---|
| [risk] | [mitigation] | [test/check] |

## Validation Strategy

- Unit:
- Integration:
- Contract:
- Manual / E2E:
- Regression:

## Task Seeds

### Seed 1: [deliverable]

**Scope**:
**Files**:
**Interfaces**:
**Validation**:
**Depends on**:

### Seed 2: [deliverable]

...

## Plan Readiness Check

- [ ] Every gap maps to at least one task seed.
- [ ] Every global constraint is copied from spec/design or explicitly decided here.
- [ ] Every changed file has a reason.
- [ ] Every produced interface has a consumer or explicit future-use rationale.
- [ ] Validation covers acceptance criteria and regression risk.
- [ ] No unresolved placeholders remain.
```

## 和当前 SpecKit 模板的差异

当前 `spec-kit/templates/plan-template.md` 仍把 `plan.md` 当综合技术上下文文档：

- `Technical Context` 容易变成 current design snapshot。
- `Project Structure` 是泛化模板树，不是本次变更 File Map。
- 没有 `Current State / Target State / Gap`。
- 没有 `Global Constraints` 作为可机械提取约束。
- 没有 per-task `Interfaces` 和 validation strategy。

如果按目标态重做，优先改语义，而不是先改文件名：

```text
design.md = design/current-target snapshot
plan.md = future implementation plan
tasks.md = generated from plan.md
```

## 最终建议

Superpowers 的经验可以压缩成一句话：

> `plan.md` 必须让执行者少猜，让 reviewer 好判断，让 `tasks.md` 能机械生成。

因此目标态应采用 Superpowers 的执行严谨性，但补上它 plan 模板里不固定的 `Current State / Target State / Gap / Risks` 字段，并把代码级步骤下沉到 `tasks.md`。
