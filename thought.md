# Thought 数据规范

Thought（想法）是**流体域**数据类型，代表用户原始输入经 clarify 后的结构化产物。生命周期始于 stdin，终于 stdout，不持久化到 gallery。

## 数据结构

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| `id` | UUID | 是 | 全局唯一标识 |
| `title` | String | 是 | 概括性标题 |
| `description` | String | 是 | 用户原始文本 |
| `created_at` | DateTime | 是 | 创建时间（RFC 3339） |

## YAML 示例

```yaml
id: d4e5f6a7-b8c9-0123-defa-234567890123
title: 建立人机协同的反思与辩论模型
description: 通过 AI 自我辩论和人类反馈的交替收敛实现高质量反思
created_at: 2026-06-09T10:30:00Z
```

## 约束

- Thought 不包含 Situation / Intention / Schema 的任何字段
- id 由服务端生成，客户端不传入
- created_at 在 clarify 时设为当前时间
- 不在 gallery 中持久化——Thought 是纯管道类型

## 与其他类型的关系

```
Thought ──clarify──→ Intention（从原始想法中提取意图）
Thought + Intention ──cluster──→ Situation（多条指向同一认知域时聚类）
```

Thought 是系统的入口：用户输入原始文本，clarify 产出一个或多个 Thought。每个 Thought 可产生 0..N 条 Intention。Thought 本身不直接关联到 Situation 或 Schema。
