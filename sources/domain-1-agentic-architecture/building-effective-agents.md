# Building Effective Agents
Source: https://www.anthropic.com/research/building-effective-agents
Published: December 19, 2024

## What Are Agents?

Two types of agentic systems:
- **Workflows**: Systems where LLMs and tools are orchestrated through predefined code paths.
- **Agents**: Systems where LLMs dynamically direct their own processes and tool usage.

## When (and When Not) to Use Agents

Start simple. Find the simplest solution possible, and only increase complexity when needed. Agentic systems trade latency and cost for better performance.

## Building Blocks & Patterns

### The Augmented LLM
The foundational building block combines LLMs with augmentations: retrieval, tools, and memory. Models can actively use these capabilities—generating their own search queries, selecting appropriate tools, and determining what information to retain.

### Workflow: Prompt Chaining
Decomposes tasks into sequential steps where each LLM call processes previous output. Programmatic checks ("gates") ensure the process stays on track.
Use cases: Marketing copy generation followed by translation; Document outline creation with validation, then full document writing.

### Workflow: Routing
Classifies an input and directs it to a specialized followup task. This enables building optimized prompts for distinct input categories.
Use cases: Directing customer service queries to appropriate workflows; Routing simple questions to cost-efficient models (Haiku) and complex ones to capable models (Sonnet).

### Workflow: Parallelization
Two variations:
- **Sectioning**: Breaking tasks into independent parallel subtasks.
- **Voting**: Running identical tasks multiple times for diverse outputs.

### Workflow: Orchestrator-Workers
A central LLM dynamically breaks down tasks, delegates them to worker LLMs, and synthesizes their results.
Key distinction from parallelization: subtasks aren't pre-defined but determined by the orchestrator based on input.
Use cases: Coding products making changes across multiple files; Search tasks gathering information from multiple sources.

### Workflow: Evaluator-Optimizer
One LLM generates responses while another evaluates and provides feedback in loops.
Use cases: Literary translation requiring nuanced feedback; Complex search tasks needing multiple rounds of analysis.

### Agents
Agents work through cycles: receive user input, plan independently, execute using tools with environmental feedback, pause for human input at checkpoints, and include stopping conditions for control.
When to use: Open-ended problems where step counts cannot be predicted and fixed paths cannot be hardcoded.

## Core Principles
1. **Simplicity**: Keep agent designs straightforward
2. **Transparency**: Explicitly show planning steps
3. **Documentation & Testing**: Carefully craft agent-computer interfaces

## Appendix 1: Agents in Practice
- **Customer Support**: Combines chatbot interfaces with tool integration. Usage-based pricing for successful resolutions.
- **Coding Agents**: Code solutions verifiable through automated tests, agents iterate using test results as feedback.

## Appendix 2: Prompt Engineering Tools
- Give models enough tokens to "think" before committing
- Keep formats close to naturally occurring internet text
- Eliminate formatting overhead
- Use clear parameter names and descriptions with examples
- Apply poka-yoke principles—make mistakes harder to make
