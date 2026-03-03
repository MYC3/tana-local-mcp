# Tana Local MCP

[English](./README.md) | [简体中文](./README.zh-CN.md)

用于将 Codex 连接到 Tana Desktop 的 Local API/MCP，并以安全的“先读后写”方式管理节点、标签与字段。

## 这个技能能做什么

- 指导配置 `tana-local` MCP（`add` + `login`）
- 通过本地健康检查脚本验证连通性
- 推荐读优先流程（`list_tags`、`search_nodes`、`read_node`）
- 覆盖常见写操作（`edit_node`、`set_field_content`、`tag` 等）

## 安装

1. 将本目录复制到你的 Codex skills 目录，例如：

```bash
cp -R tana "$CODEX_HOME/skills/tana"
```

2. 在项目的 `AGENTS.md` 中增加技能条目（名称、描述、路径）。

## 通过 skill-installer 从 GitHub 安装

如果你使用内置 `skill-installer`，可直接从本仓库安装：

```bash
# 示例：从 GitHub 仓库路径安装
# 在 Codex 的 skill-installer 流程中输入：
<owner>/tana-local-mcp
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

- 当用户要求把内容保存到 Tana，或调用 Tana 做内容记录时，默认将新增内容保存到 Tana workspace 的 `Daily Notes` 下。
- 仅当用户明确指定具体目录和 tags时，才覆盖该默认规则。

## 在提示词中使用

- “使用 `tana` 列出我的 tags”
- “使用 `tana` 读取节点 <nodeId>”

## 仓库结构

- `SKILL.md`
- `agents/openai.yaml`
- `references/tana-local-mcp-ops.md`
- `scripts/check_tana_local_api.sh`

## 许可证

MIT
