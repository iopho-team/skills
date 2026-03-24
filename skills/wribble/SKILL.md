---
name: wribble
description: wribble - The Wribble CLI for publishing blog posts and managing channels
allowed-tools: Bash(wribble *), mcp__wribble__wribble_list_posts, mcp__wribble__wribble_get_post, mcp__wribble__wribble_create_post, mcp__wribble__wribble_update_post, mcp__wribble__wribble_delete_post, mcp__wribble__wribble_search_posts, mcp__wribble__wribble_get_post_channels, mcp__wribble__wribble_assign_channels, mcp__wribble__wribble_list_channels, mcp__wribble__wribble_get_channel, mcp__wribble__wribble_create_channel, mcp__wribble__wribble_update_channel, mcp__wribble__wribble_delete_channel
user-invocable: true
argument-hint: <command> [options]
updated: "2026-03-24"
---

# wribble — Minimal Thoughts Blog CLI

Publish blog posts and manage channels from the terminal or as an AI agent.

**Install:** `npm install -g wribble`

**Auth:** Get a CLI token at `app.wribble.iopho.com → Settings → Integrations → CLI Token`, then:
```bash
wribble auth token rdk_xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

---

## Tool Preference

Use `wribble` CLI (Bash) for single-language quick posts and CRUD operations — fast, token-efficient, composable with pipes.

Use `mcp__wribble__*` MCP tools for:
- **Multilingual posts** (adding multiple language versions to one post)
- **Complex channel management workflows**

**CRITICAL — Decision Rules:**

| User intent | Action |
|---|---|
| "write / post / publish / share / note" | `wribble post` or `wribble_create_post` |
| "edit / update / revise / fix" | `wribble edit` or `wribble_update_post` |
| "add [language] version / translate" | `wribble_update_post` MCP ONLY (CLI is single-lang per call) |
| "organize / assign to channel / categorize" | `wribble channels assign` or `wribble_assign_channels` |
| "research complete / summarize findings" | Offer: "Want me to post this to your Wribble blog?" |
| NEVER post without explicit user intent | Wribble is public publishing — more invasive than saving to a library |

---

## Global Flags

| Flag | Description |
|---|---|
| `--json` | Output as JSON (for scripting / jq) |
| `--no-color` | Disable color output |

---

## Auth Commands

```bash
wribble auth token rdk_xxx        # Save PAT token
wribble auth whoami               # Verify authentication
wribble auth logout               # Remove stored credentials
```

---

## Post Commands

### Publish a post (killer feature)

```bash
# With content argument
wribble post "Hello world! #thoughts"

# From stdin (pipe)
echo "My quick thought #idea" | wribble post
cat article.md | wribble post --title "My Article"

# From file
wribble post --file notes.md --title "Weekly Notes"

# With channel assignment
wribble post "Learned something new today #learning" --channel dev-notes

# With explicit lang
wribble post "Bonjour monde" --lang fr --title "Premier post"
```

Options:
- `--title <t>` — Title (auto-derived from first non-empty line if omitted)
- `--lang <code>` — Language code (default: `en`)
- `--channel <slug>` — Assign to channel after creating
- `--file <path>` — Read content from file

Tags are **auto-extracted server-side** from `#hashtags` in content. The CLI just sends content.

### List, get, edit, delete

```bash
wribble list                          # All posts
wribble list --channel dev-notes      # Filter by channel
wribble list --limit 20 --offset 0    # Pagination

wribble get <id>                      # Full post with all language versions

wribble edit <id> --content "Updated text" --lang en
wribble edit <id> --title "New Title"
echo "New content" | wribble edit <id>    # Via stdin

wribble delete <id>                   # Prompts confirmation
wribble delete <id> --force           # Skip confirmation
```

---

## Search

```bash
wribble search "keyword"
wribble search "query" --limit 10
```

---

## Channel Commands

```bash
wribble channels                      # List all channels with post counts
wribble channels create "Dev Notes"   # Create channel (slug auto-generated)
wribble channels create "My Blog" --slug blog --description "Personal thoughts"
wribble channels assign <post-id> <slug> [<slug2> ...]   # Assign post to channels
```

---

## Multilingual Posts (MCP)

For adding multiple language versions to a single post, use the MCP tool:

```
wribble_create_post with languages: {
  "en": { "title": "Hello", "content": "English content #tag", "isOriginal": true },
  "zh": { "title": "你好", "content": "中文内容 #标签" }
}
```

To add a language version to an existing post:
```
wribble_update_post with id and languages: {
  "zh": { "title": "中文标题", "content": "中文内容" }
}
```

---

## Stdin Piping Examples

```bash
# Quick thought
echo "Just realized something important #insight" | wribble post

# Post a file with title
cat weekly-notes.md | wribble post --title "Week 12 Notes" --channel weekly

# Post command output
git log --oneline -10 | wribble post --title "Recent commits" --lang en

# Research summary → post
wribble search "previous research" | wribble post --title "Research Summary"
```

---

## Data Model

Posts have a `languages` JSON field: `{ en: { title, content, isOriginal? }, zh: { ... } }`.
Tags are auto-extracted from `#hashtags` across all language content.
Channels organize posts; posts can belong to multiple channels.
