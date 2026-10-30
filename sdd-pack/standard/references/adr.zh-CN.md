# ADR 阶段

目标：为一个长期决策创建 `docs/adr/ADR-XXXX-kebab-title.md`，并维护 `docs/adr/index.md`。

ADR 是从 plan/research 中筛选出的长期决策，不是 research 的全文复制。

## 什么时候创建 ADR

- 未来维护者会问：“为什么当时这么做？”
- 决策改变了架构、模块边界、公共接口、数据模型、部署、运行时或运维策略。
- 否决了另一个可信方案。
- 取舍会影响多个 feature 或未来实现计划。
- 决策需要长于当前 feature 的生命周期。

## 不要为这些内容创建 ADR

- 局部实现细节。
- 一次性 workaround。
- 库用法说明。
- 已经完全被当前 plan 消化的 research 结论。
- 从代码或项目约定中显而易见的选择。

## 流程

1. 明确只记录一个决策。
2. 先读取 `docs/adr/index.md`；如果不存在，用 `templates/adr-index-template.zh-CN.md` 创建。
3. 从 `docs/adr/index.md` 和 `docs/adr/ADR-*.md` 共同解析下一个 ADR 编号。
4. 使用 `templates/adr-template.zh-CN.md`。
5. 标题同时表达问题和所选方案。
6. 填写决策人、咨询人员、被通知人员和置信度。
7. 背景以一个明确决策问题收束。
8. 按重要程度排列决策驱动因素。
9. 只分析真实考虑过的可信方案。
10. 决策结果只选择一个方案，并说明理由。
11. 写清验证方式和重新评估条件。
12. 链接相关 `requirement.md`、`plan.md`、`research.md`、contracts、issues、PRs、PoC、benchmark 或 ADR。
13. 创建或更新 ADR 文件后，同步更新 `docs/adr/index.md`。
14. ADR 保持短小、稳定、可长期解释。

## Index 规则

- `docs/adr/index.md` 是 ADR 管理入口；不要为了判断已有决策而默认读取全部 ADR。
- index 必须列出 ADR 编号、日期、状态、决策摘要、置信度、文件链接、替代关系和相关资料。
- ADR 状态变化或替代关系变化时必须同步更新 index。

## 填写规则

- 不复制完整 research，只抽取决策证据。
- 不把多个独立决策塞进一份 ADR。
- 后续工作只能记录非阻塞事项；阻塞实现的内容必须回到 plan/tasks。
- 状态为 `已被替代` 时必须填写 `被替代`。
- 当前 ADR 替代旧 ADR 时必须填写 `替代`。

## 输出

- `docs/adr/index.md`
- `docs/adr/ADR-XXXX-kebab-title.md`
