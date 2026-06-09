# Situation 数据规范

Situation（情境）是**固体域**数据类型，代表"当前发生了什么"。从 gallery 中只读加载，由 intention + thought 聚类产生。

## 数据结构

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| `id` | UUID | 是 | 全局唯一标识 |
| `name` | String | 是 | 程序化标识，如 `think`、`org`、`infra` |
| `label` | String | 是 | 中文标签，如 `认知工程`、`组织管理`、`基础设施` |
| `content` | SituationContent | 是 | 情境的四个维度 |

### SituationContent

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| `agenda` | String | 是 | 目标——这个情境要达成什么 |
| `ecology` | String | 是 | 环境状态——当前发生了什么 |
| `frame` | String | 是 | 认知框架——如何理解这个情境 |
| `dynamics` | String | 是 | 演化——这个情境如何变化 |

## YAML 示例

```yaml
id: d4e5f6a7-b8c9-0123-defa-234567890123
name: think
label: 认知工程
content:
  agenda: 将意图工程确立为认知工程的核心方法论，以意图为基本单元驱动产品设计、架构设计等一切结构化生成过程。
  ecology: 人机辩论模型暴露出 AI 自收敛不跳出框架的问题、可拓展监督模式（AI 监督 AI）被验证、章程生成成为辩论的自然产出、智谱意外验证"意图工程"概念。
  frame: 将人机辩论理解为意图发现和收敛的具体手段——人类反馈是打破 AI 局部最优的关键，辩论的产物天然是章程类结构化知识，意图工程则是一切人类意图驱动生成过程的统一框架。
  dynamics: 从人机辩论与反思模型的实验，到可拓展监督模式的确立，再到意图工程概念的发现与验证，是认知工程核心方法论从工具到理论的跃迁。
```

## 存储格式

Gallery 中按周组织，每个文件对应一个 situation：

路径：`docs/gallery/situation/2026-W23/{name}.yaml`（如 `think.yaml`、`business.yaml`）

## 约束

- `name` 必须全局唯一，作为隐式关联键
- Situation 是 gallery 的入口点——review 等命令以 situation 列表为骨架展开
- Situation 本身不直接引用 Intention 或 Thought，通过 `name` 字段隐式关联

## 与其他类型的关系

```
Thought + Intention ──cluster──→ Situation（聚类）
Situation ──repeated──→ pattern ──abstract──→ Schema（模式沉淀）
```

Situation 处于认知构件的中间层——下接 Intention（的具体实例），上接 Schema（的抽象模式）。Situation 之间可存在支持/冲突/触发/演化等关系，由 analyze 命令计算。
