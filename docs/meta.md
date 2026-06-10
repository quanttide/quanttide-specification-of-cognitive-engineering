# 元数据

定义 World 和 Domain 的映射表结构。

## World

World 代表一个具备内在一致性的认知主体。数据按 world 组织，每个 world 有一份独立的时间线。

### 字段

- `name`: 必选。程序化标识，如 `founder`、`company`。
- `label`: 必选。中文标签，如 `量潮创始人`、`量潮科技`。
- `long-name`: 必选。英文标识，用于程序化引用，如 `quanttide-founder`、`quanttide-tech`。
- `parent`: 可选。父 world 的 name，用于构建层级关系。

### YAML 示例

```yaml
- name: founder
  label: 量潮创始人
  long-name: quanttide-founder

- name: company
  label: 量潮科技
  long-name: quanttide-tech
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

## 存储位置

- `docs/gallery/meta/world.yaml` — World 映射表
- `docs/gallery/meta/domain.yaml` — Domain 映射表
