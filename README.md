# Claude Certified Architect -- Study Guide

Everything you need to prepare for the **Claude Certified Architect -- Foundations** certification by Anthropic.

26 curated documents from official Anthropic sources, a scenario-based exam simulator agent, and a progress tracker.

## Exam Overview

| Domain | Weight | Topics |
|--------|--------|--------|
| Agentic Architecture & Orchestration | **27%** | Agentic loop, hub-and-spoke, subagents, hooks, enforcement |
| Tool Design & MCP Integration | **18%** | Tool descriptions, MCP primitives, error responses, tool_choice |
| Claude Code Configuration & Workflows | **20%** | CLAUDE.md hierarchy, skills, rules, plan mode, CI/CD |
| Prompt Engineering & Structured Output | **20%** | Few-shot, JSON schemas, validation loops, batch API |
| Context Management & Reliability | **15%** | Lost in the middle, escalation, error propagation, compaction |

- **Format**: 60 multiple-choice questions, scenario-based, 120 minutes
- **Passing score**: 720 / 1000
- **Scenarios**: 4 randomly selected from 6 (Customer Support, Code Generation, Multi-Agent Research, Developer Productivity, CI/CD, Data Extraction)

## Quick Start

### Installation

```bash
git clone https://github.com/eRom/claude-study-guide.git
cd claude-study-guide
```

### Take a Practice Exam

Launch the exam agent:

```bash
claude --agent cca-examiner
```

Or from within a Claude Code session, mention the agent:

```
@cca-examiner full
```

### Two Modes

| Mode | Command | Description |
|------|---------|-------------|
| **Full Exam** | `full`, `exam`, `complet` | 60 questions, 4 random scenarios, results at the end, correction report |
| **Quick** | `quick`, `rapide`, `une question` | 1 random question with immediate feedback |

### After a Full Exam

The agent automatically generates:

- **`reports/YYYY-MM-DD_HHhMM.md`** -- Detailed correction in French with sourced explanations
- **`results.md`** -- Score tracker with per-domain breakdown and progression notes

## Project Structure

```
.
|-- CLAUDE.md                    # Project context for Claude Code
|-- results.md                   # Exam score tracker
|-- reports/                     # Detailed correction reports
|-- .claude/
|   `-- agents/
|       `-- cca-examiner.md      # Exam simulator agent
`-- sources/
    |-- SOURCES_INDEX.md         # Complete index with all URLs
    |-- official-exam-guide-anthropic.pdf
    |
    |-- domain-1-agentic-architecture/
    |   |-- building-effective-agents.md
    |   |-- building-agents-with-claude-agent-sdk.md
    |   |-- multi-agent-research-system.md
    |   |-- effective-harnesses-for-long-running-agents.md
    |   |-- demystifying-evals-for-agents.md
    |   |-- agent-skills.md
    |   `-- claude-code-subagents.md
    |
    |-- domain-2-tool-design-mcp/
    |   |-- writing-tools-for-agents.md
    |   |-- advanced-tool-use.md
    |   `-- tool-use-complete.md
    |
    |-- domain-3-claude-code-config/
    |   |-- claude-code-memory.md
    |   `-- claude-code-hooks-reference.md
    |
    |-- domain-4-prompt-engineering/
    |   |-- claude-4-best-practices.md
    |   `-- structured-outputs.md
    |
    |-- domain-5-context-management/
    |   |-- effective-context-engineering.md
    |   `-- contextual-retrieval.md
    |
    |-- mastering/                # Advanced deep-dive docs
    |   |-- domain-2-tools-mcp/
    |   |   `-- code-execution-with-mcp.md
    |   |-- domain-3-claude-code/
    |   |   |-- skills-best-practices.md
    |   |   |-- complete-guide-building-skills.pdf
    |   |   `-- claude-code-sandboxing.md
    |   `-- domain-4-prompts/
    |       `-- think-tool.md
    |
    |-- exam-prep-cheatsheet-balaji.md
    `-- exam-technical-architecture-framework.md
```

## Sources

All documents are sourced from official Anthropic resources:

| Source | Documents |
|--------|-----------|
| [Anthropic Engineering Blog](https://www.anthropic.com/engineering) | Building Effective Agents, Writing Tools for Agents, Context Engineering, Multi-Agent Research, Advanced Tool Use, Evals, Think Tool, Sandboxing, etc. |
| [Claude Code Docs](https://code.claude.com/docs) | Memory/CLAUDE.md, Hooks, Subagents, Skills |
| [Claude Platform Docs](https://platform.claude.com/docs) | Prompting Best Practices, Structured Outputs, Tool Use API |
| [MCP Specification](https://modelcontextprotocol.io) | Architecture, Tools, Resources, Prompts |
| [Anthropic Academy](https://anthropic.skilljar.com) | Official courses and practice exam |
| Official Exam Guide | Anthropic's confidential NTK exam guide with all 28 task statements |

See [`sources/SOURCES_INDEX.md`](sources/SOURCES_INDEX.md) for the complete list with direct URLs.

## Key Documents to Start With

If you're short on time, read these five first:

1. **`official-exam-guide-anthropic.pdf`** -- The official exam structure, scenarios, and sample questions
2. **`exam-prep-cheatsheet-balaji.md`** -- Complete domain cheatsheet with anti-patterns and traps
3. **`domain-1/.../building-effective-agents.md`** -- THE foundational reference on agent patterns
4. **`domain-4/.../claude-4-best-practices.md`** -- Modern prompting for Claude 4.x
5. **`domain-5/.../effective-context-engineering.md`** -- Context as a finite resource

## Contributing

Found a missing official resource? Open a PR adding it to the appropriate `sources/` subdirectory and update `SOURCES_INDEX.md`.

---

*Built with [Claude Code](https://claude.ai/code) by [Romain Ecarnot](https://github.com/eRom).*
