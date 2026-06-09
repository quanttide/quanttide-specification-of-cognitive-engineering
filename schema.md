# Schema 数据规范

Schema（图式）是**固体域**数据类型，代表"认知规律是什么"。从 gallery 中只读加载，由跨 situation 重复出现的模式抽象产生。

## 数据结构

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| `id` | UUID | 是 | 全局唯一标识 |
| `name` | String | 是 | 程序化标识，与 Situation.name 对应 |
| `label` | String | 是 | 中文标签 |
| `content` | SchemaContent | 是 | 图式的详细内容 |

### SchemaContent

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| `usage` | String | 是 | 适用场景——何时使用该图式 |
| `entities` | Vec\<Entity\> | 是 | 核心概念列表 |
| `causals` | Vec\<Causal\> | 是 | 因果规则列表 |
| `boundaries` | Vec\<String\> | 是 | 边界条件列表 |
| `properties` | Vec\<KeyValue\> | 是 | 属性键值对 |
| `dynamics` | Vec\<KeyValue\> | 是 | 演化特征键值对 |
| `mappings` | Vec\<Mapping\> | 是 | intent→action 映射列表 |
| `biases` | Vec\<Bias\> | 是 | 常见偏差列表 |

### Entity

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| `name` | String | 是 | 概念名称 |
| `attributes` | Vec\<String\> | 是 | 概念的关键属性 |

### Causal

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| `condition` | String | 是 | 条件 |
| `outcome` | String | 是 | 结果 |

### KeyValue

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| `key` | String | 是 | 键 |
| `value` | String | 是 | 值 |

### Mapping

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| `intent` | String | 是 | 意图描述 |
| `action` | Value | 是 | 对应的行动（任意 JSON/YAML 值） |

### Bias

| 字段 | 类型 | 必需 | 说明 |
|------|------|------|------|
| `id` | UUID | 是 | 偏差唯一标识 |
| `belief` | String | 是 | 常见错误信念 |
| `fact` | String | 是 | 对应的事实/纠正 |

## YAML 示例

```yaml
id: a1b2c3d4-e5f6-7890-abcd-ef1234567890
name: business
label: 商务拓展
content:
  usage: 适用于产品经理和创业者评估新想法时参考
  entities:
    - name: 新想法
      attributes:
        - 可行性
        - 门槛
    - name: 验证手段
      attributes:
        - POC
        - 章程
        - 原型
  causals:
    - condition: 新想法通过低门槛验证
      outcome: 可行后结构化复制
    - condition: 验证失败
      outcome: 低成本放弃
  boundaries:
    - 适用于商业和研发探索
    - 排除高投入长期项目
    - 验证周期不超过两周
  properties:
    - key: 验证成本
      value: 低
    - key: 复制效率
      value: 高
  dynamics:
    - key: 演化方向
      value: 从单点到系统
  mappings:
    - intent: 探索新商业模式
      action: 做POC验证
    - intent: 降低风险
      action: 先小规模试错
  biases:
    - id: b1c2d3e4-f5a6-7890-bcde-f12345678901
      belief: 所有想法都值得先投入
      fact: 低门槛验证可快速筛选无效想法
    - id: b1c2d3e4-f5a6-7890-bcde-f12345678902
      belief: 验证成功就等于有商业价值
      fact: 验证成功只是技术可行，商业价值需要独立评估
```

## 存储格式

Gallery 中按周组织，一个文件含多条 schema（YAML 顶层为数组）：

路径：`docs/gallery/schema/2026-W23.yaml`

## 约束

- `name` 必须与对应的 Situation.name 一致
- Entity.attributes 当前为扁平字符串列表，未来可能进化
- Mapping.action 为 `Value` 类型（任意 JSON/YAML），不限定具体结构
- Bias.id 为 UUID，用于唯一标识每条偏差，支持去重和引用
- dynamics 字段记录演化特征（如"演化方向：从单点到系统"、"收敛速度：随反馈质量提升"），区别于 properties（静态属性）

## 与其他类型的关系

```
Situation ──repeated──→ pattern ──abstract──→ Schema（模式抽象）
Schema.mappings[].intent ←→ Intention.title（模式化总结）
```

Schema 是认知构件的顶层：多个 situation 中重复出现的 entities、causals、boundaries 等共同模式沉淀为 schema。Schema 的 mappings 字段是 intention 的模式化总结——将具体的意图归纳为可复用的 intent→action 映射。
