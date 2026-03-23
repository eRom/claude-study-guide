# Writing Effective Tools for Agents
Source: https://www.anthropic.com/engineering/writing-tools-for-agents

## What is a Tool?
Tools represent a new contract between deterministic systems and non-deterministic agents. Unlike traditional APIs, agents may call tools variably, hallucinate, or misunderstand usage.

## Core Principles for Tool Design

### 1. Choose Tools Strategically
More tools don't guarantee better outcomes. Build "thoughtful tools targeting specific high-impact workflows." Implement search-based tools rather than list-all tools. Tools can consolidate multiple operations.

### 2. Namespace Tools Clearly
Group related tools under consistent prefixes (e.g., asana_search, jira_search). This reduces confusion.

### 3. Return Meaningful Context
Prioritize "contextual relevance over flexibility." Use semantic field names (name, image_url) instead of technical identifiers (uuid, mime_type). Implement optional response_format parameters (concise/detailed).

### 4. Optimize for Token Efficiency
Implement pagination, filtering, truncation, and range selection with sensible defaults. Error messages should provide actionable improvements.

### 5. Engineer Tool Descriptions
Treat descriptions like onboarding documentation for new team members. Make implicit context explicit. Claude Sonnet 3.5 achieved SOTA SWE-bench performance after "precise refinements to tool descriptions."

## Evaluation-Driven Approach
1. Generate realistic multi-step evaluation prompts
2. Run evaluations programmatically with agentic loops
3. Review agent reasoning transcripts — "what agents omit" matters
4. Paste eval transcripts into Claude to analyze and refactor tools

## Results
Claude-optimized tools substantially outperformed human-written versions on held-out test sets for Slack and Asana.
