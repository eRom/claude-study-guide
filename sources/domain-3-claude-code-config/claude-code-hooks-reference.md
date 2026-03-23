# Claude Code Hooks Reference
Source: https://code.claude.com/docs/en/hooks

## Overview
Hooks are user-defined shell commands, HTTP endpoints, or LLM prompts that execute automatically at specific points in Claude Code's lifecycle.

## Hook Lifecycle Events

### Session-level
- SessionStart - When session begins or resumes
- SessionEnd - When session terminates

### User interaction
- UserPromptSubmit - When user submits a prompt
- InstructionsLoaded - When CLAUDE.md or rules files load

### Tool execution (agentic loop)
- PreToolUse - Before tool call executes (CAN BLOCK)
- PermissionRequest - When permission dialog appears
- PostToolUse - After tool call succeeds
- PostToolUseFailure - After tool call fails

### Agent events
- SubagentStart - When subagent spawned
- SubagentStop - When subagent finishes
- TeammateIdle - Agent team teammate about to go idle
- TaskCompleted - Task being marked completed

### Completion
- Stop - When Claude finishes responding
- StopFailure - When turn ends due to API error

### Other
- ConfigChange, PreCompact, PostCompact, WorktreeCreate, WorktreeRemove
- Elicitation, ElicitationResult (MCP)

## Hook Handler Types

### 1. Command hooks (type: "command")
Shell commands receive JSON on stdin. Exit 0 = success, Exit 2 = blocking error.

### 2. HTTP hooks (type: "http")
POST request, receive decision via response body. 2xx = success, non-2xx = non-blocking error.

### 3. Prompt hooks (type: "prompt")
Single-turn LLM evaluation. Use $ARGUMENTS for hook input JSON.

### 4. Agent hooks (type: "agent")
Spawn subagent with tools (Read, Grep, Glob) before returning decision.

## Configuration Locations
| Location | Scope |
|---|---|
| ~/.claude/settings.json | All projects |
| .claude/settings.json | Single project (shareable) |
| .claude/settings.local.json | Single project (local) |
| Managed policy settings | Organization-wide |
| Plugin hooks/hooks.json | When plugin enabled |
| Skill/agent frontmatter | Component lifetime |

## Matcher Patterns
Regex string filtering when hooks fire:
- PreToolUse/PostToolUse: Tool name (Bash, Edit, Write, mcp__.*)
- SessionStart: startup, resume, clear, compact
- MCP tools: mcp__<server>__<tool>

## PreToolUse Decision Control
```json
{
  "hookSpecificOutput": {
    "hookEventName": "PreToolUse",
    "permissionDecision": "allow|deny|ask",
    "permissionDecisionReason": "Reason",
    "updatedInput": { "field": "new value" }
  }
}
```

## Key Patterns
- Block destructive commands (grep for rm -rf, exit 2)
- Run linting after file writes (PostToolUse on Edit|Write)
- Auto-approve safe commands (npm test -> allow)
- Load context from external sources (SessionStart hook)
- Audit configuration changes (ConfigChange hook)

## Settings Resolution (priority order)
1. Managed policy (highest)
2. Local settings
3. Project settings
4. User settings
5. Plugin hooks
6. Built-in hooks (lowest)
