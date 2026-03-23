# How Claude Remembers Your Project
Source: https://code.claude.com/docs/en/memory

Two mechanisms carry knowledge across sessions:
- **CLAUDE.md files**: instructions you write
- **Auto memory**: notes Claude writes itself

## CLAUDE.md vs Auto Memory

| | CLAUDE.md files | Auto memory |
|---|---|---|
| Who writes it | You | Claude |
| What it contains | Instructions and rules | Learnings and patterns |
| Scope | Project, user, or org | Per working tree |
| Loaded into | Every session | Every session (first 200 lines) |

## CLAUDE.md File Locations

| Scope | Location | Purpose |
|---|---|---|
| Managed policy | /Library/Application Support/ClaudeCode/CLAUDE.md | Organization-wide |
| Project instructions | ./CLAUDE.md or ./.claude/CLAUDE.md | Team-shared |
| User instructions | ~/.claude/CLAUDE.md | Personal preferences |

## Writing Effective Instructions
- **Size**: target under 200 lines per CLAUDE.md file
- **Structure**: use markdown headers and bullets
- **Specificity**: concrete and verifiable ("Use 2-space indentation" not "Format code properly")
- **Consistency**: no contradicting rules

## Import Additional Files
Use @path/to/import syntax. Relative and absolute paths allowed. Max depth: 5 hops.

## Organize Rules with .claude/rules/
Place markdown files in .claude/rules/ directory. Each file = one topic.
Path-specific rules: use YAML frontmatter with paths field and glob patterns.

## Auto Memory
- Enabled by default
- Storage: ~/.claude/projects/<project>/memory/
- MEMORY.md acts as index (first 200 lines loaded)
- Topic files loaded on demand

## /init Command
Run /init to generate starting CLAUDE.md automatically.
Set CLAUDE_CODE_NEW_INIT=true for interactive multi-phase flow.

## /memory Command
Lists all loaded CLAUDE.md and rules files. Toggle auto memory. Open memory folder.
