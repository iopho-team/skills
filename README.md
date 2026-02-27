# iopho-team/skills

AI agent skills for [iopho](https://github.com/iopho-team) products. Works with Claude Code, Cursor, Windsurf, and [40+ other agents](https://skills.sh/).

## Available Skills

| Skill | Description | Install |
|-------|-------------|---------|
| [pnote](skills/pnote/) | [PromptNote](https://promptnoteapp.com/) CLI for managing prompts, notes, and snippets | `npx skills add iopho-team/skills --skill pnote` |

## Quick Install

```bash
# Install a specific skill
npx skills add iopho-team/skills --skill pnote

# Install all skills
npx skills add iopho-team/skills --all

# Global install (available across all projects)
npx skills add iopho-team/skills --skill pnote -g -y
```

## Manual Install

Each skill is a directory under `skills/` with a `SKILL.md` file. Copy the skill directory into your agent's skill folder:

- **Claude Code**: `.claude/skills/`
- **Cursor / Windsurf / Other**: `.agents/skills/`

## License

MIT
