# Intention 数据规范

Intention（意图）是**固体域**数据类型，代表"人想要达成什么"。从 gallery 中只读加载，由 thought clarify 产出。

## 数据结构

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| `id` | UUID | 是 | 全局唯一标识 |
| `title` | String | 是 | 意图标题 |
| `description` | String | 是 | 意图详述 |
| `motivation` | String | 是 | 动机——为什么有这个意图 |
| `agent` | Agent | 是 | 执行主体 |
| `level` | Level | 是 | 层次——该意图在整体中的位置 |
| `priority` | Priority | 是 | 优先级 |
| `trigger` | Trigger | 是 | 触发条件 |
| `risk` | Risk | 是 | 风险评估 |

### Agent

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| `name` | String | 是 | 程序化标识，如 `founder`、`founder_ai` |
| `label` | String | 是 | 中文标签，如 `创始人`、`创始人+AI` |

### Level / Priority / Trigger / Risk

维度类型，结构相同：

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| `name` | String | 是 | 程序化标识，如 `high`、`middle`、`persistent` |
| `label` | String | 是 | 中文标签，如 `高`、`中层`、`持续` |
| `description` | String | 是 | 说明该维度的选值原因或含义 |

## Level 枚举值

| name | label | 说明 |
|------|-------|------|
| `top` | 顶层 | 为所有意图提供元框架和方向 |
| `middle` | 中层 | 为顶层意图服务的阶段性目标 |
| `bottom` | 底层 | 日常执行层面的具体任务 |

## Priority 枚举值

| name | label | 说明 |
|------|-------|------|
| `high` | 高 | 核心假设，辐射范围最广 |
| `medium` | 中 | 重要但不紧急 |
| `low` | 低 | 远期探索，方向尚未收敛 |

## Trigger 枚举值

| name | label | 说明 |
|------|-------|------|
| `persistent` | 持续 | 直到目标达成为止 |
| `conditional` | 条件触发 | 特定条件满足时触发 |

## Risk 枚举值

| name | label | 说明 |
|------|-------|------|
| `high` | 高 | 核心假设尚未被验证 |
| `medium` | 中 | 执行层面需要校准 |
| `low` | 低 | 风险可控 |

## YAML 示例

```yaml
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

## 存储格式

Gallery 中按周组织，一个文件含多条 intention（YAML 顶层为数组）：

```yaml
- id: 2ee4bf46-...
  title: 建立人机协同的反思与辩论模型
  # ...
- id: a930f34f-...
  title: 将意图工程作为认知工程的核心方法论
  # ...
```

路径：`docs/gallery/intention/2026-W23/think.yaml`

## 约束

- `agent.name` 与 `agent.label` 的映射关系应在 `contract/domain.yaml` 中维护
- `level` / `priority` / `trigger` / `risk` 四个维度的 `name` 与 `label` + `description` 的映射关系应在 `contract/domain.yaml` 中维护
- Intention 通过 `name` 字段与 Situation 隐式关联（非编译期依赖），文件名中的 Situation name 体现关联

## 与其他类型的关系

```
Thought ──clarify──→ Intention（提取意图）
Intention ──cluster──→ Situation（多条意图指向同一认知域时聚类）
Schema.mappings[].intent ←→ Intention.title（模式化总结）
```
