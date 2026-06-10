# 元数据

定义 World 和 Domain 的映射表结构。

## World

World 代表一个具备内在一致性的认知主体。数据按 world 组织，每个 world 有一份独立的时间线。

### 字段

- `name`: 必选。程序化标识，如 `founder`、`company`。
- `label`: 必选。中文标签，如 `量潮创始人`、`量潮科技`。
- `parent`: 可选。父 world 的 name，用于构建层级关系。

### YAML 示例

```yaml
- name: founder
  label: 量潮创始人

- name: company
  label: 量潮科技
```

## Domain

Domain 代表情境的领域分类。用于将 situation 按认知域归类。

### 字段

- `name`: 必选。程序化标识，如 `think`、`org`、`product`。
- `label`: 必选。中文标签，如 `认知工程`、`组织管理`、`产品研发`。
- `parent`: 可选。父 domain 的 name，用于构建层级关系。

### YAML 示例

```yaml
- name: think
  label: 认知工程

- name: product
  label: 产品研发
  parent: think
```
