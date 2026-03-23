# The "Think" Tool: Enabling Claude to Stop and Think
Source: https://www.anthropic.com/engineering/claude-think-tool
Published: March 20, 2025

## Key Distinction
- **Extended thinking**: what Claude does BEFORE generating a response
- **Think tool**: what Claude does DURING response generation — a step to pause and reason

## Tool Definition
```json
{
  "name": "think",
  "description": "Use the tool to think about something. It will not obtain new information or change the database, but just append the thought to the log.",
  "input_schema": {
    "type": "object",
    "properties": {
      "thought": {
        "type": "string",
        "description": "A thought to think about."
      }
    },
    "required": ["thought"]
  }
}
```

## Performance Results
- **Airline domain (τ-bench)**: 0.370 -> 0.570 (+54% with optimized prompt)
- **Retail domain**: 0.783 -> 0.812
- **SWE-bench**: +1.6% improvement isolated

## Best Use Cases
1. **Tool output analysis** — processing results before next action
2. **Policy-heavy environments** — verifying compliance with detailed guidelines
3. **Sequential decision making** — multi-step processes where errors compound

## When NOT to Use
- Non-sequential tool calls
- Simple instruction following

## Update (Dec 2025)
Extended thinking now recommended over think tool in most cases. Think tool remains valuable for complex, policy-heavy agentic workflows.
