# Reliability Practices

本文件记录当前仓库改动风险较高的区域。它回答“在这个项目里，改哪些东西需要格外小心”，不重复通用可靠性建议。硬约束见 [RULES.md](../../RULES.md)。

<!-- sdd:todo-checklist:start -->
补全本文件前请确认：
- 从真实测试、hook、CI、release、兼容性、生成输出、持久数据和运维边界中提炼风险区域。
- 按影响范围和失败代价排序；不要把所有目录都列成高风险。
- 区分 command、validation 和 runner；不要把未配置检查写成 gate。
- 可执行硬约束进入 [RULES.md](../../RULES.md)，路径职责进入 [ARCHITECTURE.md](../../ARCHITECTURE.md)。
- 未确认内容保留 `[NEEDS CLARIFICATION: ...]`。
<!-- sdd:todo-checklist:end -->

## 高风险改动区域

按风险从高到低排列：

| 区域 | 影响范围 | 为什么风险高 |
|------|----------|-------------|
| [NEEDS CLARIFICATION: path or surface] | [NEEDS CLARIFICATION: 影响的用户、数据、部署、生成输出或外部集成] | [NEEDS CLARIFICATION: 失败代价、回滚难度、兼容性或安全风险] |
| [NEEDS CLARIFICATION: path or surface] | [NEEDS CLARIFICATION: 影响范围] | [NEEDS CLARIFICATION: 风险原因] |
| [NEEDS CLARIFICATION: path or surface] | [NEEDS CLARIFICATION: 影响范围] | [NEEDS CLARIFICATION: 风险原因] |

相比之下，[NEEDS CLARIFICATION: 已核实风险较低的区域] 的改动风险较低，前提是 [NEEDS CLARIFICATION: 不触碰的接口、数据、配置或外部行为边界]。

## 高风险确认边界

| 区域 | 改动前问题 | 最低验证 | 需要确认时机 |
|---|---|---|---|
| [NEEDS CLARIFICATION: 权限、安全、配置、数据、发布、生成输出或外部集成区域] | [NEEDS CLARIFICATION: 修改前必须回答的问题] | [NEEDS CLARIFICATION: 自动检查、人工核对或未绑定] | [NEEDS CLARIFICATION: 需要用户/团队确认的触发条件] |
| [NEEDS CLARIFICATION: high-risk area] | [NEEDS CLARIFICATION: pre-change question] | [NEEDS CLARIFICATION: minimum validation] | [NEEDS CLARIFICATION: confirmation trigger] |

## 改动前检查矩阵

| 场景 | 容易漏掉 | 必须同步核对 |
|------|----------|--------------|
| [NEEDS CLARIFICATION: 入口/API/CLI/UI 权限或路由] | [NEEDS CLARIFICATION: 权限、导航、文档、错误处理或兼容性不同步] | [NEEDS CLARIFICATION: 相关入口、配置、测试和用户可见输出] |
| [NEEDS CLARIFICATION: 数据模型/schema/mapper/store] | [NEEDS CLARIFICATION: 类型、查询、迁移、初始化数据或历史数据不同步] | [NEEDS CLARIFICATION: model、storage、migration、fixtures、tests] |
| [NEEDS CLARIFICATION: 模板/生成器/导出产物] | [NEEDS CLARIFICATION: 只改生成结果，不改生成源头] | [NEEDS CLARIFICATION: 生成源头、样例输出、兼容性和文档] |
| [NEEDS CLARIFICATION: 配置/部署/脚本] | [NEEDS CLARIFICATION: 本机路径、真实凭据、平台差异或启动命令漂移] | [NEEDS CLARIFICATION: 配置默认值、环境变量、脚本、CI 或 release 入口] |

## 容易放错的位置

| 场景 | 容易误放 | 正确位置 |
|---|---|---|
| [NEEDS CLARIFICATION: 新入口、新页面、新命令、新 API 或新任务] | [NEEDS CLARIFICATION: 容易误放的目录或模块] | [NEEDS CLARIFICATION: 正确目录、模块或生成源头] |
| [NEEDS CLARIFICATION: 共享类型、公共 helper、平台适配或集成代码] | [NEEDS CLARIFICATION: 容易误放的位置] | [NEEDS CLARIFICATION: 正确边界] |

## 当前验证能力

- [NEEDS CLARIFICATION: 完整验证入口，例如 `scripts/verify`、CI job 或“当前没有自动化验证”。]
- [NEEDS CLARIFICATION: 局部测试、lint、format、build、link check、migration check 或部署验证入口。]
- [NEEDS CLARIFICATION: 哪些风险只能通过 review、人工验证或 agent 执行验证。]
- 验证失败后修复问题并重新运行同一验证命令；最终交付只报告最终状态。

## 和 Rules 的关系

完成条件、runner 约束和必须始终成立的硬规则见 [RULES.md](../../RULES.md)。本文件只记录可靠性判断边界：哪里风险高、为什么高、以及当前有什么验证能力覆盖它。
