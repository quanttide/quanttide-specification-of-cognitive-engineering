# 工程标准

建模人类思考和认知模式，帮助人类重构认知和减少认知负担。

## 数据类型规范

| 类型 | 域 | 说明 | 规范 |
|------|-----|------|------|
| Thought | 流体 | 想法——原始输入的文本 | [thought.md](thought.md) |
| Intention | 固体 | 意图——人想要达成什么 | [intention.md](intention.md) |
| Situation | 固体 | 情境——当前发生了什么 | [situation.md](situation.md) |
| Schema | 固体 | 图式——认知规律是什么 | [schema.md](schema.md) |

## 构件关系

```
Thought ──clarify──→ Intention ──cluster──→ Situation ──pattern──→ Schema
                                                          ↗
                                              Intention (映射)
```

## 存储位置

- 流体数据：不持久化，stdin → stdout 管道
- 固体数据：`docs/gallery/{type}/2026-W{week}/` （intention/situation 按周、按 name 组织；schema 按周、单文件）
- 领域映射：`docs/gallery/contract/domain.yaml`
