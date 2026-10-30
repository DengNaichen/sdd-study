---
name: standard-sdd-adr
description: 当需要把一个长期 Standard SDD 架构或设计决策记录为 ADR 时使用，尤其是 plan.md 或 research.md 中出现未来维护者需要理解的长期取舍。
---

# Standard SDD ADR

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
2. 先读取 `docs/adr/index.md`；如果不存在，用 `templates/adr-index-template.zh-CN.md` 或 `templates/adr-index-template.md` 创建。
3. 从 `docs/adr/index.md` 和 `docs/adr/ADR-*.md` 共同解析下一个 ADR 编号；编号冲突时，以文件系统中已存在的最大编号为准。
4. 中文 artifact 使用 `templates/adr-template.zh-CN.md`；英文 artifact 使用 `templates/adr-template.md`。
5. 标题同时表达问题和所选方案，例如 `ADR-0002: 使用事件驱动同步订单状态`。
6. 填写参与信息：
   - 决策人：对结果负责的人或团队。
   - 咨询人员：提供输入但不最终拍板的人。
   - 被通知人员：需要知道该决策的人。
7. 填写置信度：
   - 高：已有生产经验、数据或强约束支持。
   - 中：证据足够执行，但仍有可验证风险。
   - 低：需要 PoC、实验或后续复查；必须写重新评估条件。
8. 背景与问题以一个清晰决策问题收束。
9. 决策驱动因素按重要程度排序，不要写成普通背景列表。
10. 方案分析只写真实考虑过的可信方案；`保持现状` 只有在确实可行时才保留。
11. 决策结果必须只选择一个方案，并说明为什么拒绝其他方案。
12. 验证方式写可执行检查；不适用的类别写 `N/A`，不要留空。
13. 重新评估条件写具体触发器，例如成本、规模、失败率、团队约束或外部依赖变化。
14. 链接相关 `requirement.md`、`plan.md`、`research.md`、contracts、issues、PRs、PoC、benchmark 或 ADR。
15. 创建或更新 ADR 文件后，立即更新 `docs/adr/index.md` 中对应行。

## Index 规则

- `docs/adr/index.md` 是 ADR 管理入口；不要为了判断已有决策而默认读取全部 ADR。
- index 必须列出 ADR 编号、日期、状态、决策摘要、置信度、文件链接、替代关系和相关资料。
- 新增 ADR 时添加一行。
- ADR 状态变化时同步更新 index。
- ADR 被替代时，同时更新新旧 ADR 在 index 里的 `替代` / `被替代` 字段。
- index 的决策摘要只写一句话，不复制 ADR 正文。

## 填写规则

- 不要复制完整 research；只抽取决策所需证据。
- 不要把多个独立决策塞进一份 ADR。
- 后续工作只能记录非阻塞事项；阻塞实现的内容必须回到 plan/tasks。
- 如果状态是 `已被替代`，必须填写 `被替代`。
- 如果当前 ADR 替代旧 ADR，必须填写 `替代`。
- ADR 保持短小、稳定、可长期解释。

## 输出

- `docs/adr/index.md`
- `docs/adr/ADR-XXXX-kebab-title.md`
