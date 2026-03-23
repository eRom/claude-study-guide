# Effective Context Engineering for AI Agents
Source: https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
Published: September 29, 2025

## Context Engineering vs Prompt Engineering
Context engineering encompasses strategies for curating and maintaining the optimal token set during LLM inference. It goes beyond prompts to include system instructions, tools, MCP, external data, and message history.

## Why Context Engineering Matters
- "Context rot": as token counts increase, models' recall accuracy decreases
- LLMs have an "attention budget" that depletes with each token
- Transformers: n² pairwise relationships creates natural tension between context size and attention focus
- Performance gradient, not hard cliff

## The Anatomy of Effective Context

### System Prompts
- Find the Goldilocks zone between over-specification (brittle) and under-specification (vague)
- Organize with XML tags or Markdown headers
- Start minimal, add based on identified failure modes

### Tools
- Self-contained, robust to error, clear intended use
- Curate minimal viable tool sets (avoid bloat with overlapping functionality)
- If human engineers can't specify which tool applies, agents can't either

### Examples
- Few-shot prompting remains strongly-advised best practice
- Curate diverse, canonical examples rather than stuffing edge cases
- For LLMs, examples function as "pictures" worth thousands of words

## Context Retrieval and Agentic Search
Shift from pre-inference retrieval to "just in time" context strategies:
- Maintain lightweight identifiers (file paths, queries, links)
- Dynamically load data using tools
- Claude Code: targeted queries, Bash commands (head, tail) — never loads full objects into context
- Hybrid strategies: retrieve some upfront, explore more autonomously

## Context Engineering for Long-Horizon Tasks

### Compaction
- Summarize conversations approaching context limits
- Preserve architectural decisions, unresolved bugs, implementation details
- Discard redundant tool outputs
- Tool result clearing: one of the safest, lightest-touch compaction forms

### Structured Note-Taking (Agentic Memory)
- Agents regularly write notes persisted outside context windows
- Example: Claude Code creating to-do lists, maintaining NOTES.md
- Claude playing Pokémon: tracks 1,234+ game steps with precise tallies

### Sub-Agent Architectures
- Specialized sub-agents with clean context windows
- Each subagent may use tens of thousands of tokens but returns condensed summaries (1,000-2,000 tokens)
- Clear separation of concerns

## Choosing the Right Approach
- **Compaction**: maintains conversational flow
- **Note-taking**: excels for iterative development with clear milestones
- **Multi-agent**: handles complex research and analysis
