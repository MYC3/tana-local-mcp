# tana-api-manager

[English](./README.md) | [简体中文](./README.zh-CN.md)

Connect Codex to Tana Desktop Local API/MCP for safe read/write workflows on nodes, tags, and fields.

## What this skill does

- Guides setup of `tana-local` MCP (`add` + `login`)
- Verifies connectivity with a local health check script
- Recommends read-first workflows (`list_tags`, `search_nodes`, `read_node`)
- Covers write workflows (`edit_node`, `set_field_content`, `tag`, etc.)

## Install

1. Copy this folder into your Codex skills directory, for example:

```bash
cp -R tana-api-manager "$CODEX_HOME/skills/tana-api-manager"
```

2. Add a skill entry in your project's `AGENTS.md` (name, description, file path).

## Install via skill-installer (GitHub)

If you use the built-in `skill-installer`, install directly from this repo:

```bash
# Example: install from GitHub repo path
# Use the skill-installer workflow in Codex and provide:
MYC3/tana-api-manager
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

## Usage in prompts

- "Use `tana-api-manager` to list tags"
- "Use `tana-api-manager` to read node <nodeId>"

## Repository layout

- `SKILL.md`
- `agents/openai.yaml`
- `references/tana-local-mcp-ops.md`
- `scripts/check_tana_local_api.sh`

## License

MIT
