# drains-claude-plugin

Claude Code plugin for [SkunkWorks Logs](https://github.com/kabeer11000/skunkworks-logs-mcp) — engineering drain/entry log server.

## Installation

Copy or symlink this repo into your Claude Code plugins directory:

```
~/.claude/plugins/drains/
```

Or add to your `settings.json` to pull from this repo:

```json
{
  "pluginRegistry": {
    "drains": "https://github.com/kabeer11000/drains-claude-plugin"
  }
}
```

## Prerequisites

Configure the MCP server first:

```json
{
  "mcpServers": {
    "skunkworks-logs": {
      "command": "npx",
      "args": ["-y", "skunkworks-logs-mcp"]
    }
  }
}
```

And set env vars:
- `SKUNKWORKS_API_URL` — your SkunkWorks Logs instance URL
- `SKUNKWORKS_API_TOKEN` — your account API token

## Contents

```
skills/drains/
  SKILL.md          — main entry point
  REFERENCE.md      — tool parameter reference
  docs/
    conventions.md  — id formats, pills, ownership
```
