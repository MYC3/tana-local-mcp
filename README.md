# Tana Local MCP

[English](./README.md) | [简体中文](./README.zh-CN.md)

Connect Codex to Tana Desktop Local API/MCP for safe read/write workflows on nodes, tags, and fields.

## What this skill does

- Guides setup of `tana-local` MCP (`add` + `login`)
- Verifies connectivity with a local health check script
- Recommends read-first workflows (`list_tags`, `search_nodes`, `read_node`)
- Covers write workflows (`edit_node`, `set_field_content`, `tag`, etc.)

## Available tools

### Read

- `list_workspaces` — List available workspaces
- `search_nodes` — Search using structured queries
- `read_node` — Read node content as markdown
- `get_children` — Get paginated children of a node
- `list_tags` — List tags in a workspace
- `get_tag_schema` — Get field definitions for a tag

### Mutation

- `import_tana_paste` — Import hierarchical content
- `tag` — Add/remove tags from nodes
- `set_field_option` — Set dropdown field values
- `set_field_content` — Set text/number/date field values
- `create_tag` — Create new tags
- `add_field_to_tag` — Add fields to tags
- `set_tag_checkbox` — Configure checkbox behavior
- `check_node` / `uncheck_node` — Mark nodes done/not done
- `trash_node` — Move node to trash
- `get_or_create_calendar_node` — Get/create calendar nodes
- `edit_node` — Edit a node's name and/or description using search-and-replace

## Install

1. Copy this folder into your Codex skills directory, for example:

```bash
cp -R tana "$CODEX_HOME/skills/tana"
```

2. Add a skill entry in your project's `AGENTS.md` (name, description, file path).

## Install via skill-installer (GitHub)

If you use the built-in `skill-installer`, install directly from this repo:

```bash
# Example: install from GitHub repo path
# Use the skill-installer workflow in Codex and provide:
<owner>/tana-local-mcp
```

## Prerequisites

1. Tana Desktop running
2. `Local API/MCP server (Alpha)` enabled in Tana Labs
3. MCP server configured:

```bash
codex mcp add tana-local --url http://localhost:8262/mcp
```

4. OAuth login completed:

```bash
codex mcp login tana-local
```

## Quick check

```bash
scripts/check_tana_local_api.sh
```

Expected: JSON with `"status":"ok"`.

## Default Save Behavior

- When users ask to save content to Tana or record notes via Tana, default to creating content under Tana workspace `Daily Notes`.
- Override this default only if the user explicitly specifies a concrete directory and tags.

## Usage in prompts

- "Use `tana` to list tags"
- "Use `tana` to read node <nodeId>"

## Repository layout

- `SKILL.md`
- `agents/openai.yaml`
- `references/tana-local-mcp-ops.md`
- `scripts/check_tana_local_api.sh`

## License

MIT
