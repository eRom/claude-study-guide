# Claude Certified Architect - Index des Sources

> Toutes les ressources officielles Anthropic pour la certification, organisees par domaine.

## DOMAIN 1: Agentic Architecture & Orchestration (27%)

### Articles & Blog Posts (sauvegardés localement)
- `domain-1-agentic-architecture/building-effective-agents.md` - **THE** reference sur les patterns d'agents (Dec 2024)
- `domain-1-agentic-architecture/building-agents-with-claude-agent-sdk.md` - Agent SDK, boucle agentique, tools
- `domain-1-agentic-architecture/effective-harnesses-for-long-running-agents.md` - Multi-context window, initializer + coding agent
- `domain-1-agentic-architecture/multi-agent-research-system.md` - Orchestrator-worker, lead agent + subagents
- `domain-1-agentic-architecture/demystifying-evals-for-agents.md` - Evaluations d'agents, single vs multi-turn
- `domain-1-agentic-architecture/agent-skills.md` - Framework Agent Skills, progressive disclosure

### Documentation (sauvegardée localement)
- `domain-1-agentic-architecture/claude-code-subagents.md` - Documentation complete subagents
- `domain-1-agentic-architecture/claude-code-hooks.md` - Reference complete hooks

### URLs à consulter en ligne
- https://code.claude.com/docs/en/agent-teams - Agent teams
- https://code.claude.com/docs/en/common-workflows - Worktrees, orchestration
- https://code.claude.com/docs/en/sdk - Agent SDK overview
- https://code.claude.com/docs/en/sdk/subagents - SDK subagents

---

## DOMAIN 2: Tool Design & MCP Integration (18%)

### Articles & Blog Posts (sauvegardés localement)
- `domain-2-tool-design-mcp/writing-tools-for-agents.md` - Tool descriptions, eval-driven design
- `domain-2-tool-design-mcp/advanced-tool-use.md` - Tool Search, Programmatic Tool Calling, Examples

### Documentation (sauvegardée localement)
- `domain-2-tool-design-mcp/tool-use-complete.md` - Documentation complète tool use API (86KB)

### URLs à consulter en ligne - MCP Specification
- https://modelcontextprotocol.io/docs/learn/architecture - Architecture MCP
- https://modelcontextprotocol.io/specification/2025-06-18/server/tools - Tools spec
- https://modelcontextprotocol.io/specification/2025-06-18/server/resources - Resources spec
- https://modelcontextprotocol.io/specification/2025-06-18/server/prompts - Prompts spec
- https://modelcontextprotocol.io/specification/2025-06-18/basic - Protocol basics
- https://modelcontextprotocol.io/docs/develop/build-server - Build MCP server
- https://modelcontextprotocol.io/docs/develop/build-client - Build MCP client
- https://modelcontextprotocol.io/docs/sdk - MCP SDKs

### URLs à consulter en ligne - Claude Code MCP
- https://code.claude.com/docs/en/mcp - MCP in Claude Code

---

## DOMAIN 3: Claude Code Configuration & Workflows (20%)

### Documentation (sauvegardée localement)
- `domain-3-claude-code-config/claude-code-memory.md` - CLAUDE.md hierarchy, auto memory, rules
- `domain-3-claude-code-config/claude-code-hooks-reference.md` - Reference complete hooks (copie)

### URLs à consulter en ligne
- https://code.claude.com/docs/en/settings - Settings hierarchy
- https://code.claude.com/docs/en/skills - Skills / slash commands
- https://code.claude.com/docs/en/cli-reference - CLI reference, plan mode
- https://code.claude.com/docs/en/github-actions - CI/CD GitHub Actions
- https://code.claude.com/docs/en/security - Security model
- https://code.claude.com/docs/en/permissions - Permissions tiers
- https://code.claude.com/docs/en/sessions - Session management
- https://code.claude.com/docs/en/plugins - Plugins system

### Blog Posts
- https://www.anthropic.com/news/how-anthropic-teams-use-claude-code
- https://www.anthropic.com/news/skills - Agent Skills announcement

---

## DOMAIN 4: Prompt Engineering & Structured Output (20%)

### Documentation (sauvegardée localement)
- `domain-4-prompt-engineering/claude-4-best-practices.md` - **THE** reference prompting Claude 4.x
- `domain-4-prompt-engineering/structured-outputs.md` - JSON outputs, strict tool use, schemas

### URLs à consulter en ligne
- https://platform.claude.com/docs/en/docs/build-with-claude/prompt-engineering/multishot-prompting - Few-shot
- https://platform.claude.com/docs/en/docs/build-with-claude/prompt-engineering/chain-of-thought - CoT
- https://platform.claude.com/docs/en/docs/build-with-claude/prompt-engineering/chain-prompts - Chaining
- https://platform.claude.com/docs/en/docs/build-with-claude/prompt-engineering/use-xml-tags - XML tags
- https://platform.claude.com/docs/en/docs/build-with-claude/extended-thinking - Extended thinking
- https://platform.claude.com/docs/en/docs/build-with-claude/adaptive-thinking - Adaptive thinking
- https://platform.claude.com/docs/en/docs/build-with-claude/prompt-caching - Prompt caching
- https://platform.claude.com/docs/en/prompt-library/library - Prompt Library

---

## DOMAIN 5: Context Management & Reliability (15%)

### Articles & Blog Posts (sauvegardés localement)
- `domain-5-context-management/effective-context-engineering.md` - Context engineering complet
- `domain-5-context-management/contextual-retrieval.md` - RAG, Contextual Embeddings + BM25

### URLs à consulter en ligne
- https://platform.claude.com/docs/en/docs/build-with-claude/token-counting - Token counting
- https://platform.claude.com/docs/en/docs/build-with-claude/prompt-engineering/long-context-tips - Long context
- https://platform.claude.com/docs/en/api/errors - API errors
- https://platform.claude.com/docs/en/api/rate-limits - Rate limits
- https://platform.claude.com/docs/en/api/handling-stop-reasons - Stop reasons
- https://www.anthropic.com/news/claude-2-1-prompting - Lost in the middle research

---

## CROSS-DOMAIN: Ressources generales

### Formation & Certification
- https://www.anthropic.com/learn - Anthropic Learn
- https://www.anthropic.com/learn/build-with-claude - Academy: API Development Guide
- https://platform.claude.com/docs/en/docs/resources/courses - Courses listing

### API Core
- https://platform.claude.com/docs/en/docs/about-claude/models/overview - Models overview
- https://platform.claude.com/docs/en/api/messages - Messages API
- https://platform.claude.com/docs/en/api/overview - API overview

### Cookbooks (GitHub)
- https://github.com/anthropics/anthropic-cookbook - Anthropic Cookbook
- https://github.com/anthropics/anthropic-cookbook/tree/main/patterns/agents - Agent patterns
