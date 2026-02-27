# pnote

[![npm](https://img.shields.io/npm/v/pnote)](https://www.npmjs.com/package/pnote)

Claude Code skill for [PromptNote](https://promptnoteapp.com/) CLI.

## Installation

### Option A: Via skills.sh (Recommended)

**Interactive** (choose agents and confirm):
```bash
npx skills add iopho-team/skills --skill pnote
```

**Non-interactive** (install to all agents, skip prompts):
```bash
npx skills add iopho-team/skills --skill pnote --all
```

**Global install** (user-level, available across all projects):
```bash
npx skills add iopho-team/skills --skill pnote -g -y
```

### Option B: Manual Installation

#### 1. Install the CLI

```bash
npm install -g pnote
```

#### 2. Authenticate

Get your Personal Access Token from [PromptNote Settings](https://app.promptnoteapp.com/settings), then:

```bash
pnote auth token pn_your_token_here
```

#### 3. Use the Skill

In Claude Code, use `/pnote` to invoke:

```
/pnote notes
/pnote search "AI art"
/pnote snippet copy abc123
```

## What This Skill Does

This skill wraps the `pnote` CLI to let Claude help you:

- **List and search** your notes and snippets
- **Read and copy** prompt content to clipboard
- **Create and manage** notes, tags, and versions
- **Access PIN-protected** notes securely

## CLI Commands

| Command | Description |
|---------|-------------|
| `pnote notes` | List all notes |
| `pnote notes get <id>` | Get note with snippet |
| `pnote search <query>` | Search notes and snippets |
| `pnote snippet copy <id>` | Copy snippet to clipboard |
| `pnote tags` | List all tags |

See `pnote --help` for full documentation.

## Links

- [PromptNote App](https://app.promptnoteapp.com/)
- [Documentation](https://www.promptnoteapp.com/docs/)
- [Feedback & Bugs](https://iohpo.featurebase.app/?b=695f9152f13092ad189fb4de)

## License

MIT
