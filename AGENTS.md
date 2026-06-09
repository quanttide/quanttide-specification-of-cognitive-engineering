# AGENTS.md

本仓库是认知工程的数据模型规范，定义四种认知构件的数据结构、字段约束和序列化格式。

## 文件

- `docs/index.md`：首页，规范概述。
- `docs/thought.md`：想法数据规范。
- `docs/intention.md`：意图数据规范，含维度枚举。
- `docs/situation.md`：情境数据规范。
- `docs/schema.md`：图式数据规范，含子类型。

## 文件结构

- `AGENTS.md`、`README.md` 位于根目录。
- 内容文档位于 `docs/` 目录。
- 根目录预留空间给未来新增的契约文件（`contract/`）、映射表（`registry/`）等其他格式的资源。

## 规范

- 字段定义使用 `- \`field\`: 必选/推荐/可选. Description.` 格式。
- 枚举值列出 name / label / 说明 三元组。
- YAML 示例放在文末 `## YAML示例` 节，使用 `#` 注释。

## 变更

- 修改规范后先提交推送本仓，再更新主仓库的子模块指针。
