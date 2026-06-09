# 情境关系

情境关系（SituationRelation）代表两个情境之间的关联。情境不孤立存在——共享概念、认知框架或意图链的两个情境之间存在可分类的关系。

## 字段

- `source`: 必选。源情境名称，对应 Situation.name。
- `target`: 必选。目标情境名称，对应 Situation.name。
- `relation_type`: 必选。关系类型枚举值。
- `confidence`: 必选。证据置信度，`high` 或 `low`。
- `description`: 必选。关系说明，描述为什么两个情境存在该关系。

## 关系类型

| name | label | 说明 |
|------|-------|------|
| `support` | 支持 | 源情境为 target 提供资源或前提 |
| `conflict` | 冲突 | 源情境与 target 存在目标或方法冲突 |
| `trigger` | 触发 | 源情境的变化导致 target 的响应 |
| `evolve` | 演化 | target 是源情境在时间上的延续 |

## 置信度

- `high`：多个证据维度（共享实体 + 共享认知框架 + 意图链）同时成立。
- `low`：仅一个证据维度成立。

## YAML 示例

```yaml
# 单条关系
source: think
target: product
relation_type: support
confidence: high
description: 认知工程的方法论产出直接驱动产品研发的交互范式设计，共享"意图驱动"和"人机协作"核心概念。
```
