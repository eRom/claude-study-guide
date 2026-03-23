# How Anthropic Built Their Multi-Agent Research System
Source: https://www.anthropic.com/engineering/multi-agent-research-system

## Core Architecture
Orchestrator-worker pattern: lead agent coordinates while spawning specialized subagents in parallel.

## Key Performance Finding
Multi-agent system with Opus 4 as lead + Sonnet 4 subagents outperformed single-agent Opus 4 by 90.2%.
Token usage explains ~80% of performance variance.

## Eight Prompting Principles
1. Develop mental models of agent behavior through Console simulations
2. Provide explicit delegation guidance with clear objectives and task boundaries
3. Embed scaling rules based on query complexity
4. Design tools carefully with distinct purposes and clear descriptions
5. Leverage model self-improvement by having Claude suggest prompt refinements
6. Start broad, then narrow search strategies progressively
7. Use extended thinking as a controllable planning scratchpad
8. Implement parallel tool calling to dramatically reduce research time

## Evaluation Strategy
LLM judges assessing: factual accuracy, citation accuracy, completeness, source quality, tool efficiency.
Human testing remains essential for catching edge cases.

## Production Challenges
- Agents require stateful execution with graceful error recovery
- Non-deterministic behavior complicates debugging
- Early agents favored SEO content over authoritative academic sources (corrected via prompts)
