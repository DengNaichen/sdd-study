# SDD 流程决策点

## 已对齐决策

| 维度 | 可选值 | 要回答的问题 |
|---|---|---|
| 范围 | 产品级、系统级、变更级、发布级、执行级 | 它描述哪个范围？ |
| 信息类型 | 需求、设计、决策、计划、任务、证据、记录、参考、债务 | 它承载什么信息？ |
| 权威性 | authoritative、derived、informational | 它是否是该事实的权威来源？ |
| 生命周期 | living、immutable record、generated、transient | 它需要持续维护、冻结保留、重新生成，还是删除？ |



2. 软需 / SRS 写法

FR-LOGIN-001：发送验证码
用户输入合法的中国大陆手机号并点击“获取验证码”后，系统应向该手机号发送 6 位数字验证码。

输入：11 位手机号。
前置条件：手机号格式合法，用户已勾选用户协议。
输出：发送成功提示，并开始 60 秒倒计时。

规则：

* 验证码有效期为 5 分钟；
* 同一手机号 60 秒内不得重复发送；
* 同一手机号每天最多发送 10 次；
* 验证码连续输错 5 次后，本验证码失效；
* 短信发送失败时，页面提示“验证码发送失败，请稍后重试”。

验收条件：

* 输入合法手机号时可以成功发送验证码；
* 60 秒内再次点击不能重复发送；
* 验证码过期后不能用于登录；
* 正确验证码登录成功；
* 未注册手机号登录后自动创建账户。

软需重点是明确、完整、可开发、可测试。开发和测试人员看完后，不应再猜“有效期多久”“错误几次失效”。

### 1. 执行过程应保持轻量

`spec`、`plan`、`tasks` 主要服务一次变更的对齐、规划和执行，不应默认都沉淀为长期资产。

目标不是生产一整套永久文档，而是让一次变更可以被清楚执行、验证，并把真正有长期价值的知识留下来。

**按稳定的业务能力归类，按可观察、可测试的系统行为命名，不按类名、服务名或代码包名划分。**


### 2. Spec 可以存在，但不是唯一长期资产；软需需要长期保留

`spec` 的主要作用是对齐用户目标、场景、需求和验收标准。

它可以保留，但不应承载架构、实现计划、任务拆解和所有历史细节。只有仍有产品或验收价值的内容才需要长期维护。

`软需` 介于 `spec` 和 PRD 之间：它不是一次执行任务，也不只是低层实现细节，而是对产品/业务/体验/约束有长期解释价值的需求资产。

`软需` 需要沉淀和保留。

### 3. Spec / Plan / Tasks 可以一起进入历史快照，但不作为长期 source of truth

以下内容默认是执行介质：

- `spec.md`
- `plan.md`
- `tasks.md`
- agent task brief
- agent report
- review package
- progress ledger

`spec.md`、`plan.md`、`tasks.md` 可以作为一次 feature/change 的历史快照一起保留，方便回溯当时为什么这么做。

但历史快照不等于长期维护对象。执行结束后，长期 source of truth 应回流到 ADR、软需、技术债 tracker、领域模型或代码本身。

### 4. 长期资产要分层，不是所有设计产物都必须保留

长期资产不应是“能生成什么就保留什么”。应按价值分层。

必须沉淀：

- ADR
- 重要 trade-off
- 架构设计
- 关键技术决策
- `软需`
- 长期技术债务 tracker（先用 Markdown）

按需沉淀：

- 领域模型 / `data-model.md`
- 已验证的不变量
- 重要限制和约束

不一定沉淀：

- `contracts/`
- 可从代码、类型、schema、OpenAPI、测试或工具稳定生成的文档

原则：如果代码已经是最可靠的 source of truth，就不要再维护一份容易漂移的长期文档。需要文档时可以生成；需要沉淀的是生成不出来的判断、取舍和债务。

ADR 是直接引入的长期资产。ADR 需要能引用具体代码位置，并在必要时直接引用关键代码块，避免只留下抽象结论。

### 5. Plan 是 future implementation plan，不是 current design snapshot

`plan.md` 描述一次变更如何落地。

它可以引用当前状态和目标状态，但目的只是支持执行，不是替代设计文档。

### 7. 执行后需要知识回流

实现完成后，应主动判断哪些内容需要沉淀：

- 用户目标或验收变化 -> 更新 `spec`
- 架构变化 -> 更新 ADR，必要时同步 `design.md`
- 接口变化 -> 优先让代码、类型、schema 或测试成为 source of truth；只有人工消费价值明确时才保留 `contracts/`
- 领域概念变化 -> 视稳定性更新 `data-model.md`
- 关键取舍 -> 记录 ADR
- 技术债 -> 进入 Markdown 技术债 tracker
- `软需` -> 进入长期软需记录
- 纯执行步骤 -> 保留在历史快照或 scratch，不长期维护

### 8. 需要一个长期技术债务 tracker

技术债不应该散落在 plan、tasks、review comment 或聊天记录里。

先用 Markdown 作为长期技术债务 tracker，用来记录：

- 债务是什么
- 为什么现在不解决
- 影响范围
- 触发条件或还债时机
- 当前 owner / 状态
- 相关 ADR、PR、issue 或代码位置

这个 tracker 是长期资产，但它不等于执行计划。它记录“未来必须记得的债”，不记录一次变更的每个执行步骤。

### 9. 从 SpecKit 和 Superpowers 吸收机制，不吸收完整文档负担

从 SpecKit 吸收的是组织和生成机制：

- feature workspace：给一次变更一个清晰工作区
- `spec.md`：用于轻量 intent / acceptance 对齐
- `data-model.md`：作为按需沉淀的领域模型位置
- `contracts/`：作为可生成接口参考的组织位置，不默认手写长期维护
- task generation：从执行计划生成任务
- hooks / extension：作为流程扩展机制

从 Superpowers 吸收的是执行纪律：

- execution plan 要可执行
- file map 替代泛化项目结构
- global constraints 要可机械提取
- per-task interfaces 降低跨任务漂移
- review gates 保证执行质量
- scratch execution state 支持恢复，但不进入长期资产

不照搬：

- 把所有执行细节长期化
- 让 plan 变成超长执行脚本
- 强制所有团队使用 subagent-per-task
- 把 current design snapshot 直接转 tasks
- 把 generated contracts 当成必须手写维护的 source of truth

## 推荐流程

```text
Intent alignment
  -> lightweight execution planning
  -> task generation
  -> implementation and verification
  -> historical snapshot: spec + plan + tasks
  -> durable knowledge capture: ADR / 软需 / Markdown debt tracker / data model as needed
```

## 推荐文档分层

| 层级 | 文档/产物 | 生命周期 |
|---|---|---|
| Historical snapshot | `spec.md`, `plan.md`, `tasks.md` | 可一起保留，默认不长期维护 |
| Soft requirements | `软需` | 必须长期保留 |
| Durable decisions | ADR with code references / code blocks | 必须长期保留 |
| Architecture | `design.md` or equivalent architecture notes | 按重要性长期保留 |
| Domain model | `data-model.md` | 按稳定性长期保留 |
| Generated references | `contracts/`, generated schemas, API docs | 可生成，不默认长期手写维护 |
| Technical debt | Markdown debt tracker | 长期资产 |
| Execution | active `plan.md`, active `tasks.md` | 一次性执行介质 |
| Scratch | briefs, reports, review packages, progress ledger | 临时状态 |

## 剩余待定问题

1. knowledge capture 是否需要一个显式命令或 checklist。
2. Markdown 技术债 tracker 的文件路径和字段格式。
3. ADR 的模板字段，尤其代码引用和代码块引用格式。
4. `contracts/` 什么时候需要生成，什么时候完全以代码为准。
