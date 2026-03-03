# Tana Local MCP

[English](./README.md) | [简体中文](./README.zh-CN.md)

用于将 Codex 连接到 Tana Desktop 的 Local API/MCP，并以安全的“先读后写”方式管理节点、标签与字段。

## 这个技能能做什么

- 指导配置 `tana-local` MCP（`add` + `login`）
- 通过本地健康检查脚本验证连通性
- 推荐读优先流程（`list_tags`、`search_nodes`、`read_node`）
- 覆盖常见写操作（`edit_node`、`set_field_content`、`tag` 等）

## 可用工具

### 读取（Read）

- `list_workspaces` — 列出可用工作区
- `search_nodes` — 用结构化查询搜索节点
- `read_node` — 以 Markdown 读取节点内容
- `get_children` — 分页读取节点子项
- `list_tags` — 列出工作区中的 tags
- `get_tag_schema` — 获取 tag 的字段定义

### 变更（Mutation）

- `import_tana_paste` — 导入层级化内容
- `tag` — 给节点添加/移除 tags
- `set_field_option` — 设置下拉字段值
- `set_field_content` — 设置文本/数字/日期字段值
- `create_tag` — 创建新 tag
- `add_field_to_tag` — 为 tag 添加字段
- `set_tag_checkbox` — 配置复选框行为
- `check_node` / `uncheck_node` — 标记节点完成/未完成
- `trash_node` — 将节点移入回收站
- `get_or_create_calendar_node` — 获取/创建日历节点
- `edit_node` — 通过 search-and-replace 编辑节点标题和/或描述

## 安装

1. 将技能目录复制到你的 Codex skills 目录，例如：

```bash
cp -R skills/tana "$CODEX_HOME/skills/tana"
```

2. 在项目的 `AGENTS.md` 中增加技能条目（名称、描述、路径）。

## 通过 skill-installer 从 GitHub 安装

如果你使用内置 `skill-installer`，可直接从本仓库安装：

```bash
# 示例：从 GitHub 仓库路径安装
# 在 Codex 的 skill-installer 流程中输入：
<owner>/tana-local-mcp，并指定 path 为 `skills/tana`
```

## 前置条件

1. Tana Desktop 保持运行
2. 在 Tana Labs 开启 `Local API/MCP server (Alpha)`
3. 配置 MCP 服务：

```bash
codex mcp add tana-local --url http://localhost:8262/mcp
```

4. 完成 OAuth 登录授权：

```bash
codex mcp login tana-local
```

## 快速检查

```bash
scripts/check_tana_local_api.sh
```

期望输出：包含 `"status":"ok"` 的 JSON。

## 默认保存行为

- 当用户要求把内容保存到 Tana，或调用 Tana 做内容记录时，默认写入该 workspace 当天的 Daily Notes 日历节点：先用 `get_or_create_calendar_node`（`granularity: "day"`）获取/创建 day node，再用 `import_tana_paste` 写入该节点。
- 仅当用户明确指定具体目录和 tags 时，才覆盖该默认规则。

## 在提示词中使用

- 使用/选择 “Tana Local MCP” 命令执行
- 如果新线程里 `/Tana Local MCP` 没出现，可用 `$Tana Local MCP <content>` 显式调用。

## 仓库结构

- `skills/tana/SKILL.md`
- `skills/tana/agents/openai.yaml`
- `skills/tana/references/tana-local-mcp-ops.md`
- `skills/tana/scripts/check_tana_local_api.sh`

## 许可证

MIT
