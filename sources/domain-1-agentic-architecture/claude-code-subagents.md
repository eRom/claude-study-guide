# Create Custom Subagents
Source: https://code.claude.com/docs/en/sub-agents

## What Are Subagents?
Specialized AI assistants with own context window, custom system prompt, specific tool access, independent permissions.

Benefits:
- Preserve context (keep exploration out of main conversation)
- Enforce constraints (limit tools)
- Reuse configurations across projects
- Specialize behavior with focused system prompts
- Control costs (route to cheaper models like Haiku)

## Built-in Subagents

| Agent | Model | Tools | Purpose |
|---|---|---|---|
| Explore | Haiku (fast) | Read-only | File discovery, code search |
| Plan | Inherits | Read-only | Codebase research for planning |
| General-purpose | Inherits | All tools | Complex multi-step tasks |

## Subagent File Format
Markdown files with YAML frontmatter:
```yaml
---
name: code-reviewer
description: Reviews code for quality and best practices
tools: Read, Glob, Grep
model: sonnet
---
System prompt goes here in the body.
```

## Frontmatter Fields
| Field | Required | Description |
|---|---|---|
| name | Yes | Unique identifier (lowercase, hyphens) |
| description | Yes | When to delegate |
| tools | No | Tool allowlist (inherits all if omitted) |
| disallowedTools | No | Tool denylist |
| model | No | sonnet, opus, haiku, full ID, or inherit |
| permissionMode | No | default, acceptEdits, dontAsk, bypassPermissions, plan |
| maxTurns | No | Maximum agentic turns |
| skills | No | Skills to preload |
| mcpServers | No | MCP servers (inline or reference) |
| hooks | No | Lifecycle hooks scoped to subagent |
| memory | No | Persistent memory: user, project, or local |
| background | No | true = always run in background |
| effort | No | low, medium, high, max |
| isolation | No | worktree = isolated git worktree |

## Subagent Scope (priority order)
1. --agents CLI flag (session only, highest priority)
2. .claude/agents/ (project)
3. ~/.claude/agents/ (user)
4. Plugin agents/ directory (lowest)

## Invoking Subagents
- **Natural language**: "Use the test-runner subagent to fix failing tests"
- **@-mention**: @"code-reviewer (agent)" guarantees execution
- **Session-wide**: claude --agent code-reviewer

## Foreground vs Background
- **Foreground**: blocks main conversation, permissions passed through
- **Background**: concurrent, auto-denies unpre-approved permissions

## Persistent Memory
| Scope | Location |
|---|---|
| user | ~/.claude/agent-memory/<name>/ |
| project | .claude/agent-memory/<name>/ |
| local | .claude/agent-memory-local/<name>/ |

When enabled: system prompt includes memory instructions, MEMORY.md first 200 lines loaded, Read/Write/Edit tools auto-enabled.

## Key Patterns
- **Isolate high-volume operations**: test runs, log processing stay in subagent context
- **Parallel research**: spawn multiple subagents for independent investigations
- **Chain subagents**: sequential workflow, results pass between subagents
- **Restrict capabilities**: Agent(worker, researcher) syntax in tools field

## Subagents Cannot
- Spawn other subagents (no nesting)
- Use hooks from plugins (security)
