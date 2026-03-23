# Technical Architecture and Resource Framework for the CCA Foundations Certification
Source: NotebookLM research synthesis

## Exam Overview
- Proctored, 120-minute assessment
- 60 multiple-choice questions in realistic production scenarios
- Minimum 6 months hands-on experience with Claude API recommended
- Scaled score of 720 on 100-1,000 range

## Domain Weights

| Domain | Name | Weight | Key Pillars |
|---|---|---|---|
| 1 | Agentic Architecture & Orchestration | 27% | Hub-and-spoke, subagent context isolation, loop state |
| 2 | Claude Code Configuration & Workflows | 20% | CLAUDE.md hierarchy, skill frontmatter, CI/CD |
| 3 | Prompt Engineering & Structured Output | 20% | Tool use, validation-retry loops, programmatic enforcement |
| 4 | Tool Design & MCP Integration | 18% | MCP servers, transport mechanisms, dynamic tool discovery |
| 5 | Context Management & Reliability | 15% | Prompt caching, Batch API, compaction, token optimization |

## Domain 1: Agentic Architecture
- Coordinator-subagent model (hub-and-spoke)
- Subagents do NOT inherit conversation history
- stop_reason "tool_use" -> continue loop; "end_turn" -> terminate
- effort parameter balances reasoning depth vs token costs
- Agent teams coordinate across separate sessions; subagents within single session

## Domain 2: Claude Code Configuration
- CLAUDE.md = project's technical lead (arch rules, naming, build standards)
- Keep under 200 lines for max adherence
- .claude/rules/ directory for path-scoped instructions (YAML frontmatter)
- Skills = on-demand loaded, reduce base context size
- CI/CD: CLAUDE_CODE_CI_MODE=true, Docker isolation, structured JSON output

## Domain 3: Prompt Engineering & Structured Output
- Programmatic enforcement > prompt guidance (non-zero failure rate unacceptable)
- tool_use with JSON schemas = reliable structured output (no syntax errors)
- But does NOT prevent semantic errors
- Validation-retry feedback loops for schema corrections
- Multi-pass review: generator instance + separate reviewer instance

## Domain 4: Tool Design & MCP
- MCP = "USB-C port for AI" — three primitives: tools, resources, prompts
- Transport: stdio or HTTP/SSE
- Tool descriptions with input formats + explicit use-case boundaries
- Permission-based architecture for sensitive operations
- Managed MCP: allowlists/denylists for organization-wide standards

## Domain 5: Context Management & Reliability

### Prompt Caching Pricing

| Cache Type | Lifetime | Write Price | Read Price | Use Case |
|---|---|---|---|---|
| Standard | 5 min | 1.25x Base | 0.1x Base | Active multi-turn conversations |
| Extended | 1 hour | 2.0x Base | 0.1x Base | Large knowledge bases, infrequent tools |

### Batch API
- 50% token discount
- Up to 24h processing, no guaranteed SLA
- No multi-turn tool calling within single request
- Use for: overnight reports, weekly audits, nightly test generation
- NOT for: blocking pre-merge checks, live customer interactions

### Compaction
- Server-side for Opus and Sonnet 4.6
- Auto-summarizes earlier conversation parts at context limit

## Exam Scenarios Deep Dives

### Customer Support Resolution Agent
- Intelligence Layer (intent detection) + Decision Layer (risk assessment)
- Structured handoff protocols (human agent doesn't see AI conversation)
- Programmatic tool interceptors for financial limits (refund > $500 -> human)

### Multi-Agent Research System
- Lead orchestrator (Opus 4.6) + specialized researchers (Sonnet 4.6)
- Manage scraping problems, graceful fallbacks for blocked sites
- Deep research task: $1-$5 per query depending on complexity

### Claude Code for CI/CD
- Containerized Claude Code step analyzing git diffs
- Breaking API change detection (current vs base branch OpenAPI spec)
- Skills returning structured JSON for downstream CI steps

## Preparation Strategy
- Experienced devs: 2-4 weeks
- New to Claude: 2-4 months building real projects
- Complete official practice exam on Skilljar (60 questions, same scenario format)
- Courses at https://anthropic.skilljar.com/

## Key Resources
- Anthropic Academy: https://anthropic.skilljar.com/
- AI Fluency: https://www.anthropic.com/learn/claude-for-you
- Prompt Engineering Tutorial: https://github.com/anthropics/prompt-eng-interactive-tutorial
- Claude 4 Migration Guide: https://platform.claude.com/docs/en/about-claude/models/migration-guide
- Trust Center: https://www.anthropic.com/trust
