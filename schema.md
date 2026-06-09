# 图式

图式（Schema）代表"认知规律是什么"。属于固体域，从 gallery 中只读加载，由跨 situation 重复出现的模式抽象产生。

## 字段

- `id`: 必选。UUID 格式的唯一标识。
- `name`: 必选。程序化标识，与对应的 Situation.name 一致。
- `label`: 必选。中文标签。
- `content`: 必选。图式内容，包含以下字段：
  - `usage`: 必选。适用场景描述。
  - `entities`: 必选。核心概念列表，每项包含：
    - `name`: 必选。概念名称。
    - `attributes`: 必选。关键属性列表。
  - `causals`: 必选。因果规则列表，每项包含：
    - `condition`: 必选。条件。
    - `outcome`: 必选。结果。
  - `boundaries`: 必选。边界条件列表。
  - `properties`: 必选。属性键值对列表，每项包含 `key` 和 `value`。
  - `dynamics`: 必选。演化特征键值对列表，每项包含 `key` 和 `value`。
  - `mappings`: 必选。intent→action 映射列表，每项包含：
    - `intent`: 必选。意图描述。
    - `action`: 必选。对应的行动（任意 JSON/YAML 值）。
  - `biases`: 必选。常见偏差列表，每项包含：
    - `id`: 必选。UUID，唯一标识。
    - `belief`: 必选。错误信念。
    - `fact`: 必选。事实纠正。

## 存储格式

Gallery 中按周组织，一个文件含多条 schema（YAML 顶层为数组）。路径为 `docs/gallery/schema/2026-W{week}.yaml`。

## YAML 示例

```yaml
# 单条图式
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
  causals:
    - condition: 新想法通过低门槛验证
      outcome: 可行后结构化复制
  boundaries:
    - 适用于商业和研发探索
    - 排除高投入长期项目
  properties:
    - key: 验证成本
      value: 低
  dynamics:
    - key: 演化方向
      value: 从单点到系统
  mappings:
    - intent: 探索新商业模式
      action: 做POC验证
  biases:
    - id: b1c2d3e4-f5a6-7890-bcde-f12345678901
      belief: 所有想法都值得先投入
      fact: 低门槛验证可快速筛选无效想法
```
