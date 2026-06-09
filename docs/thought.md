# 想法

想法（Thought）是用户原始输入的结构化产物。

## 字段

- `id`: 必选。UUID 格式的唯一标识。
- `title`: 必选。概括性标题。
- `description`: 必选。用户原始文本。
- `created_at`: 必选。创建时间，RFC 3339 格式。

## YAML 示例

```yaml
# 单个想法
id: d4e5f6a7-b8c9-0123-defa-234567890123
title: 建立人机协同的反思与辩论模型
description: 通过 AI 自我辩论和人类反馈的交替收敛实现高质量反思
created_at: 2026-06-09T10:30:00Z
```
