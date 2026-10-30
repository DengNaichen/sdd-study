# sdd-pack Validation

本文件是当前仓库的 Validation Spec：说明有哪些验证项、证据来源、runner 绑定、trigger 状态和 receipt 行为。它不是规则索引；硬约束放在 [RULES.md](../RULES.md)，操作入口放在 [AGENTS.md](../AGENTS.md)。

不要假设仓库使用 Git、SVN、pre-commit、CI 或平台 gate。只有从真实配置、脚本、清单、runner、receipt 或团队确认中核对过的检查，才能写成已配置 validation。

<!-- sdd:todo-checklist:start -->
补全本文件前请确认：

- 每个 validation item 都有 evidence path 或团队确认来源。
- 未绑定的检查标记为 `unknown`、`absent` 或 `manual`，不要写成强制完成条件。
- Runner 只执行已经确认的质量保障命令；不要从模板示例推断目标仓库支持 lint、test、build 或 coverage。
- Trigger / Binding 只记录已经配置的入口；第一版默认只有 local manual runner 和可选 agent skill trigger，不默认 hook、CI 或 platform gate。
<!-- sdd:todo-checklist:end -->

## Model

- **Validation**：需要检查什么，例如 format、lint、typecheck、test、build、docs 或 security checks。
- **Runner**：实际执行 validation 的命令或脚本，例如 [`scripts/verify`](../scripts/verify)。
- **Runner config**：runner 读取的动态配置，例如 [`.sdd/validation.json`](../.sdd/validation.json)。
- **Trigger / Binding**：谁触发 runner，例如 agent skill、人工本地命令、hook、CI 或 platform gate。
- **Receipt**：runner 写出的执行证据，例如 `.sdd/receipts/latest.json`。

## Validation Items

| Item | Status | Command / source | Evidence | Notes |
| --- | --- | --- | --- | --- |
| Setup | [NEEDS CLARIFICATION: configured / absent / manual / unknown] | [NEEDS CLARIFICATION: command or N/A] | [NEEDS CLARIFICATION: path or team confirmation] | [NEEDS CLARIFICATION: prerequisites] |
| Format | [NEEDS CLARIFICATION: configured / absent / manual / unknown] | [NEEDS CLARIFICATION: command or N/A] | [NEEDS CLARIFICATION: path or team confirmation] | [NEEDS CLARIFICATION: runner binding] |
| Lint | [NEEDS CLARIFICATION: configured / absent / manual / unknown] | [NEEDS CLARIFICATION: command or N/A] | [NEEDS CLARIFICATION: path or team confirmation] | [NEEDS CLARIFICATION: runner binding] |
| Typecheck | [NEEDS CLARIFICATION: configured / absent / manual / unknown] | [NEEDS CLARIFICATION: command or N/A] | [NEEDS CLARIFICATION: path or team confirmation] | [NEEDS CLARIFICATION: runner binding] |
| Tests | [NEEDS CLARIFICATION: configured / absent / manual / unknown] | [NEEDS CLARIFICATION: command or N/A] | [NEEDS CLARIFICATION: path or team confirmation] | [NEEDS CLARIFICATION: scope] |
| Build | [NEEDS CLARIFICATION: configured / absent / manual / unknown] | [NEEDS CLARIFICATION: command or N/A] | [NEEDS CLARIFICATION: path or team confirmation] | [NEEDS CLARIFICATION: output / artifact risk] |
| Docs / links | [NEEDS CLARIFICATION: configured / absent / manual / unknown] | [NEEDS CLARIFICATION: command or N/A] | [NEEDS CLARIFICATION: path or team confirmation] | [NEEDS CLARIFICATION: when required] |

## Runner

Primary runner: [`scripts/verify`](../scripts/verify), backed by [`scripts/verify.cjs`](../scripts/verify.cjs).

Runner config: [`.sdd/validation.json`](../.sdd/validation.json). The default config has `checks: []`; fill it only with repository-confirmed validation commands.

Runner requirements:

- Execute only repository-confirmed validation commands.
- Read checks from runner config; do not infer commands from repository type, package manager, VCS, or template examples.
- Write receipts to `.sdd/receipts/latest.json` and `.sdd/receipts/runs/<run_id>.json`.
- Return `passed` only when every configured check passes.
- Return `failed` only when a configured command exits nonzero.
- Return `not_configured` when no runner or checks are configured.
- Return `skipped` only when a trigger intentionally skips validation and records the reason.

## Triggers / Bindings

| Trigger | Status | Command / behavior | Evidence |
| --- | --- | --- | --- |
| Agent skill | optional | If the current agent runtime provides `$code-change-verification`, it should call the configured runner. | Runtime capability, not a repository fact unless a local skill exists. |
| Local manual | configured | `scripts/verify` or `node scripts/verify.cjs` from the repository root. | `scripts/verify`, `scripts/verify.cjs`, `.sdd/validation.json` |
| Hook | [NEEDS CLARIFICATION: configured / absent / unknown] | [NEEDS CLARIFICATION: hook command or N/A] | [NEEDS CLARIFICATION: hook config path] |
| CI / platform gate | [NEEDS CLARIFICATION: configured / absent / unknown] | [NEEDS CLARIFICATION: job / gate name or N/A] | [NEEDS CLARIFICATION: workflow or platform evidence] |

## Receipts

Expected latest receipt: `.sdd/receipts/latest.json`

Expected historical receipts: `.sdd/receipts/runs/<run_id>.json`

Before checks are configured, running the default runner writes a `not_configured` receipt. That status means no repository-confirmed checks are configured; it is not a validation pass or quality failure.

Minimum receipt fields:

```json
{
  "schema_version": 1,
  "run_id": "...",
  "trigger": "agent-skill",
  "mode": "full",
  "status": "passed",
  "config_path": ".sdd/validation.json",
  "started_at": "...",
  "finished_at": "...",
  "checks": [
    {
      "name": "<confirmed-check-name>",
      "command": "<confirmed validation command>",
      "status": "passed",
      "exit_code": 0
    }
  ]
}
```

## Recursion Guard

- Hook bindings must not call commands that recursively trigger the same hook.
- Full verification must not rely on hook side effects unless the hook is explicitly part of the verified runner.
- Agent-triggered validation should report the runner mode and receipt path, not infer success from planned commands.

## Reporting

When reporting validation status, distinguish:

- `passed`: configured checks ran and passed.
- `failed`: configured checks ran and at least one failed.
- `not_configured`: runner or checks are missing; this is not a quality failure.
- `skipped`: validation was intentionally skipped with a reason.
- `not_run`: validation was applicable but not executed.
