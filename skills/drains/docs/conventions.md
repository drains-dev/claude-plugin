# Conventions

## ID Formats

Storage uses `entry:` and `drain-` prefixes. **All tool interfaces use bare ids.**

| Storage | API |
|---------|-----|
| `entry:01AR3N9K6F8...` | `01AR3N9K6F8...` |
| `drain-myproject` | `myproject` |

Always strip prefixes. All entry ids returned by `list_entries` and `append_entry`
are already bare.

## Mention Pills

`@user@example.com` — must be a real email format. Renders as a clickable pill.

## Reference Pills

| Syntax | Renders as |
|--------|------------|
| `[[dbName]]` | Link to a drain |
| `[[dbName#entryId]]` | Link to a specific entry |

No validation at write time. Invalid refs render as broken pills.

## Entry Attribution

Entries created via API token show `via <token name>` attribution — not the
account holder's name. GitHub-ingested entries show a GitHub badge.

## Ownership

| Action | Who |
|--------|-----|
| Read entries | All drain members |
| Append entries | All drain members |
| Edit / Delete | Only the entry's original author |

## Ingestion Events (GitHub webhook)

When a drain owner configures a GitHub webhook pointing at `/api/ingest/:token`,
these events are automatically logged as entries:

- `push` — each commit
- `pull_request` — open/close/merge
- `issues` — open/close/reopen

Claude does not need to take action for these — they appear automatically.
