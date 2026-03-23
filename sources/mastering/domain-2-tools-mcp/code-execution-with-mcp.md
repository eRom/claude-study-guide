# Code Execution with MCP: Building More Efficient Agents
Source: https://www.anthropic.com/engineering/code-execution-with-mcp

## Problem
1. Tool definitions overload context windows when loaded upfront
2. Intermediate results must pass through model repeatedly

Example: Google Drive to Salesforce — 2-hour meeting transcript = 50,000 extra tokens passing through twice.

## Solution: Code Execution API
Instead of direct tool calls, present MCP servers as code APIs. Agents write code to interact with tools.

Token savings: 150,000 -> 2,000 tokens (98.7% reduction).

## Key Benefits
1. **Progressive disclosure** — tools load on-demand
2. **Data filtering** — results processed in execution environment before reaching model
3. **Control flow efficiency** — loops/conditionals execute natively
4. **Privacy preservation** — sensitive data stays in execution env, PII can be tokenized
5. **State persistence** — agents maintain progress, develop reusable skills

## Tradeoff
Code execution requires secure sandboxing, resource limits, and monitoring — adds operational overhead vs direct tool calls.
