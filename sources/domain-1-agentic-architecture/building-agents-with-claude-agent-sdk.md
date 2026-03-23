# Building Agents with the Claude Agent SDK
Source: https://claude.com/blog/building-agents-with-the-claude-agent-sdk

## Overview
Anthropic renamed the Claude Code SDK to the Claude Agent SDK, reflecting its broader applicability beyond coding tasks.

## Core Design Principle
Give Claude the same tools programmers use daily: file access, terminal commands, code execution, and iteration capabilities.

## Agent Loop Framework (4-step feedback cycle)
1. **Gather context** - Search files, retrieve information
2. **Take action** - Execute tools, generate code, run commands
3. **Verify work** - Check output quality
4. **Repeat** - Iterate until success

## Key Capabilities

### Context Gathering
- Agentic search using file systems and bash commands
- Semantic search for faster retrieval
- Subagents for parallel processing and isolated context windows
- Automatic context compaction for long-running agents

### Action Taking
- Custom tools for primary workflows
- Bash scripting for flexible computer access
- Code generation for complex, reliable operations
- MCP for standardized API integrations

### Verification Methods
- Rule-based feedback (linting, validation)
- Visual feedback (screenshots, renders)
- LLM-as-judge for fuzzy evaluations
