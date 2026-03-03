# Tana Local MCP Ops

## Setup Checklist

1. Ensure Tana Desktop is running.
2. Enable `Local API/MCP server (Alpha)` in Tana Labs.
3. Add server in Codex:

```bash
codex mcp add tana-local --url http://localhost:8262/mcp
```

4. Authenticate:

```bash
codex mcp login tana-local
```

5. Smoke check MCP tools by listing available tools in Codex.

## Common Operation Patterns

### 1) Read-first discovery

1. `list_workspaces`
2. `list_tags`
3. `search_nodes`
4. `read_node`

### 2) Node content update

1. Find node with `search_nodes`
2. Confirm details with `read_node`
3. Update text/title via `edit_node`
4. Update structured fields via `set_field_content` or `set_field_option`

### 3) Supertag management

1. Inspect existing tags with `list_tags`
2. Read schema by `get_tag_schema`
3. Add new supertag with `create_tag` if missing
4. Extend fields via `add_field_to_tag`
5. Apply tag to nodes via `tag`

## Troubleshooting

- Connection refused:
  - Tana Desktop is closed, or Local API/MCP not enabled.
- Auth not completed:
  - Re-run `codex mcp login tana-local` and approve in Tana Desktop.
- Tools missing:
  - Restart Codex session after MCP add/login.
