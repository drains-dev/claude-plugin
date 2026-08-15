---
name: drains
description: "Drains — engineering log. Use whenever working on a project, investigating a problem, making decisions, or when asked about 'what happened' / 'what was decided' / 'what shipped'. Each project/team has its own drain; Claude reads it for context before starting and appends entries as work progresses. Set DRAINS_API_URL and DRAINS_API_TOKEN to use."
homepage: https://github.com/drains-dev/mcp
---

# Drains

Engineering log that lives alongside your work — a running record every project,
incident, and team writes to. Claude uses it as **persistent memory**: read before
starting work, append as you go.

## How Claude uses this

### Before starting work on a project
Call `list_drains` → find the project's drain → `list_entries` to read prior
context (decisions, incidents, what shipped). This is the first thing to do
when picking up a task.

### As work progresses
Append entries after every meaningful action: decisions made, paths taken,
problems solved, tradeoffs weighed. Think "what would a human engineer write
in the project log right now?"

Example triggers:
- Decision: "Chose Postgres over SQLite because X"
- Problem solved: "Root cause was Y, fixed by Z"
- Tradeoff: "Skipped A to ship B, revisit when X"
- Completion: "Shipped feature X, notable: Y"

### When asked about past events
`list_entries` on the relevant drain(s) → search for the topic. Drains
aggregate human notes, GitHub events (push/PR/issue), and AI entries in one
timeline.

### Day-end or week-end
`summarize_day` to condense a set of entries into one summary entry at the top.

## Drain-per-project convention

When `list_drains` doesn't show a drain for the current project:
- **Trivial / clear** (e.g., new git repo with no existing drain): create one named after the project/repo, visibility `private` unless you know it needs to be shared. Use the current working directory or repo name as the title.
- **Ambiguous**: ask the user — "no drain found for this project, shall I create one? what should it be called and who should have access?"

Claude should not begin work on a project without checking its drain first.

## Content conventions (write these exactly)

- `@user@example.com` — mention a person (renders as a pill)
- `[[dbName]]` — link to another drain
- `[[dbName#entryId]]` — link to a specific entry

Invalid references render as broken pills, not errors. No existence check at write time.

## ID rules

All tool inputs/outputs use **bare ids** (no `entry:` or `drain-` prefix).
Strip prefixes before passing ids back to other tools.

## Ownership

`edit_entry` and `delete_entry` only work on entries Claude's account created.
Claude can read all entries in a shared drain but only edit/delete its own.

## GitHub ingestion (if configured on the drain)

Push events, PRs, and issues are automatically ingested as entries by the
drain's webhook — no action needed from Claude for those.
