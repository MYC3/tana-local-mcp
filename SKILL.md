---
name: tana
description: Connect Codex to Tana via the local MCP server in Tana Desktop to get authorized read/write access, then search/read/edit nodes and manage supertags/fields using MCP tools. Use when tasks involve Tana integration setup, local API authentication, structured note sync, supertag schema updates, or node lifecycle operations.
---

# Tana Local MCP

Use this skill to configure and operate Tana's Local API/MCP from Codex with safe read/write workflows.

## Quick Start (Local MCP)

1. Open Tana Desktop.
2. Enable `Local API/MCP server (Alpha)` in Tana Labs.
3. Add the MCP server in Codex:
   - `codex mcp add tana-local --url http://localhost:8262/mcp`
4. Authenticate if needed:
   - `codex mcp login tana-local`
5. Verify MCP tools are available and run read operations first.

## 中文最短 SOP

1. 打开 Tana Desktop，在 Labs 开启 `Local API/MCP server (Alpha)`。
2. 在终端执行：`codex mcp add tana-local --url http://localhost:8262/mcp`。
3. 执行：`codex mcp login tana-local`，并在 Tana 弹窗中完成授权。
4. 连通性检查：`scripts/check_tana_local_api.sh`。
5. 先读后写：先用 `list_tags` / `search_nodes` / `read_node` 确认目标，再用 `edit_node`、`set_field_content`、`create_tag`、`add_field_to_tag`、`tag` 执行变更。

## 常见问题（简版）

- 连接失败：确认 Tana Desktop 在运行，且 Labs 开关已开启。
- 授权失败：重新执行 `codex mcp login tana-local` 并在 Tana 重新授权。
- 工具不可见：重启 Codex 会话后重试。

## Connection Details

- MCP URL: `http://localhost:8262/mcp`
- Health check (no auth): `http://localhost:8262/health`
- API docs (no auth): `http://localhost:8262/docs`
- OpenAPI spec (no auth): `http://localhost:8262/openapi.json`

Notes:

- Tana Desktop must stay running while using MCP tools.
- Authentication is OAuth approval in Tana Desktop, not static API token.

## Capability Workflow

1. Run connectivity check (`/health`) when setup changes.
2. Confirm read scope with:
   - `list_workspaces`
   - `search_nodes` / `read_node`
3. Confirm write scope with a low-risk operation:
   - `edit_node` on a disposable test node.
4. Execute task workflows for nodes and supertags.

## Node Workflows

- Discover target: `search_nodes`
- Read details: `read_node`, `get_children`
- Update content: `edit_node`, `set_field_content`, `set_field_option`
- State changes: `check_node`, `uncheck_node`, `trash_node`

## Supertag Workflows

- Discover tags: `list_tags`
- Inspect schema: `get_tag_schema`
- Create tag: `create_tag`
- Extend schema: `add_field_to_tag`, `set_tag_checkbox`
- Apply/remove tags on nodes: `tag`

## Safety Rules

- Validate read access before write actions.
- Test mutations on disposable nodes first.
- Keep bulk edits scoped by explicit search filters.
- Use `trash_node` only after confirming node identity from `read_node`.
- For save-or-record requests, create new content under Tana workspace `Daily Notes` by default.
- If user explicitly specifies a concrete directory and tags, follow the user-specified destination and tags instead.

## References

- See operational checklist and examples in `references/tana-local-mcp-ops.md`.
