# drains-claude-plugin

Claude Code plugin for [Drains](https://github.com/drains-dev/mcp) — engineering log server.

## Installation

Copy or symlink this repo into your Claude Code plugins directory:

```
~/.claude/plugins/drains/
```

Or add to your `settings.json` to pull from this repo:

```json
{
  "pluginRegistry": {
    "drains": "https://github.com/drains-dev/claude-plugin"
  }
}
```

## Prerequisites

Configure the MCP server first:

```json
{
  "mcpServers": {
    "drains": {
      "command": "npx",
      "args": ["-y", "github:drains-dev/mcp"]
    }
  }
}
```

And set env vars:
- `DRAINS_API_URL` — your Drains instance URL
- `DRAINS_API_TOKEN` — your account API token

## Contents

```
skills/drains/
  SKILL.md          — main entry point
  REFERENCE.md      — tool parameter reference
  docs/
    conventions.md  — id formats, pills, ownership
```
