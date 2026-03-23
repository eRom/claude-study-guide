# Advanced Tool Use on the Claude Developer Platform
Source: https://www.anthropic.com/engineering/advanced-tool-use

## 1. Tool Search Tool
Problem: 5-server setup (GitHub, Slack, Sentry, Grafana, Splunk) consumes ~55K tokens before conversation begins.
Solution: Mark tools with defer_loading: true for on-demand discovery. Claude only sees tools it needs.
Results: Opus 4 accuracy: 49% -> 74%, Opus 4.5: 79.5% -> 88.1%.
Best for: Tool definitions >10K tokens, systems with 10+ tools, MCP architectures.

## 2. Programmatic Tool Calling
Problem: Traditional tool calling creates context pollution and requires multiple inference passes.
Solution: Claude writes Python code calling multiple tools in sequence/parallel, processes outputs directly, returns only final results.
Results: Token consumption reduced from 43,588 to 27,297 (37% reduction).
Best for: Processing large datasets, multi-step workflows (3+ dependent calls), parallel operations.

## 3. Tool Use Examples
Problem: JSON schemas define structure but cannot express usage patterns.
Solution: Provide sample tool calls directly in tool definitions.
Results: Accuracy improved from 72% to 90% on complex parameter handling.
Best for: Tools with complex nested structures, many optional parameters, domain-specific conventions.

## Getting Started
Beta header: betas=["advanced-tool-use-2025-11-20"]
