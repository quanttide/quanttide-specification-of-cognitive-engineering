# 意图

意图（Intention）代表"人想要达成什么"。

## 字段

- `id`: 必选。UUID 格式的唯一标识。
- `title`: 必选。意图标题。
- `description`: 必选。意图详述。
- `motivation`: 必选。动机，为什么有这个意图。
- `agent`: 必选。执行主体，包含以下字段：
  - `name`: 必选。程序化标识，如 `founder`。
  - `label`: 必选。中文标签，如 `创始人`。
- `level`: 必选。层次，包含 `name`、`label`、`description`。
- `priority`: 必选。优先级，包含 `name`、`label`、`description`。
- `trigger`: 必选。触发条件，包含 `name`、`label`、`description`。
- `risk`: 必选。风险评估，包含 `name`、`label`、`description`。

## 维度枚举

`level`（层次）：

- `top` / `顶层`：为所有意图提供元框架和方向
- `middle` / `中层`：为顶层意图服务的阶段性目标
- `bottom` / `底层`：日常执行层面的具体任务

`priority`（优先级）：

- `high` / `高`：核心假设，辐射范围最广
- `medium` / `中`：重要但不紧急
- `low` / `低`：远期探索，方向尚未收敛

`trigger`（触发条件）：

- `persistent` / `持续`：直到目标达成为止
- `conditional` / `条件触发`：特定条件满足时触发

`risk`（风险）：

- `high` / `高`：核心假设尚未被验证
- `medium` / `中`：执行层面需要校准
- `low` / `低`：风险可控

## 存储格式

Gallery 中按周组织，一个文件含多条 intention（YAML 顶层为数组）。路径为 `docs/gallery/intention/2026-W{week}/{situation_name}.yaml`。

## YAML 示例

```yaml
# 单条意图
id: 2ee4bf46-9b9c-4a34-979d-f88c84ebb714
title: 建立人机协同的反思与辩论模型
description: 通过 AI 自我辩论和人类反馈的交替收敛实现高质量反思
motivation: 发现 AI 自收敛会困在局部最优，人类反馈能跳出框架
agent:
  name: founder_ai
  label: 创始人+AI
level:
  name: middle
  label: 中层
  description: 为顶层意图服务的阶段性目标
priority:
  name: high
  label: 高
  description: 可拓展监督模式被验证有效，推动认知方法论落地
trigger:
  name: persistent
  label: 持续
  description: 直到辩论模型可稳定产出章程
risk:
  name: medium
  label: 中
  description: 人类介入的时机和频率仍需校准
```
