# SkunkWorks Logs — Tool Reference

## Drain Management

### `list_drains`
```
input: {}
```

### `create_drain`
```
input: {
  title: string,
  visibility: "private" | "shared",
  description?: string,
  tags?: string[]
}
```

### `update_drain`
```
input: {
  dbName: string,
  title?: string,
  description?: string,
  tags?: string[]
}
```

### `invite_member` — shared drains, owner-only
```
input: { dbName: string, email: string }
```

### `list_members`
```
input: { dbName: string }
```

### `remove_member` — owner-only
```
input: { dbName: string, email: string }
```

---

## Entries

### `list_entries`
```
input: {
  dbName: string,
  limit?: number,      // default 50
  before?: string      // last entry id from previous page
}
```

### `append_entry`
```
input: {
  dbName: string,
  content: string      // supports @mentions and [[references]]
}
```

### `edit_entry` — own entries only
```
input: { dbName: string, entryId: string, content: string }
```

### `delete_entry` — own entries only
```
input: { dbName: string, entryId: string }
```

### `summarize_day`
```
input: { dbName: string, entryIds: string[] }
```

---

## Key rules

- **Bare ids only** — never pass `entry:` or `drain-` prefixes
- **@mentions** — `@user@example.com` (must be valid email format)
- **[[references]]** — `[[dbName]]` or `[[dbName#entryId]]`
- **edit/delete** — only works on entries your token's account created
- **Pagination** — `before` takes the last entry id from the previous page
