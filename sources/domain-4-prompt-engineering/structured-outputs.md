# Structured Outputs
Source: https://platform.claude.com/docs/en/docs/build-with-claude/structured-outputs

## Overview
Two complementary features:
- **JSON outputs** (output_config.format): Get Claude's response in a specific JSON format
- **Strict tool use** (strict: true): Guarantee schema validation on tool names and inputs

## Why Use Structured Outputs
- Always valid: No more JSON.parse() errors
- Type safe: Guaranteed field types and required fields
- Reliable: No retries needed for schema violations

## JSON Outputs

### How It Works
1. Define your JSON schema (standard JSON Schema format)
2. Add output_config.format parameter with type: "json_schema"
3. Parse response from response.content[0].text

### SDK Helpers
- Python: client.messages.parse() with Pydantic models
- TypeScript: client.messages.parse() with Zod schemas + zodOutputFormat()
- Ruby: output_config: {format: Model} with BaseModel classes
- Java: StructuredMessageCreateParams with class types

### SDK Schema Transformation
SDKs automatically:
1. Remove unsupported constraints (minimum, maximum, minLength)
2. Update descriptions with constraint info
3. Add additionalProperties: false to all objects
4. Validate responses against original schema (with all constraints)

### Common Use Cases
- Data extraction from unstructured text
- Classification with structured categories
- API response formatting

## Strict Tool Use

### Why It Matters for Agents
Without strict mode, Claude might return incompatible types ("2" instead of 2) or missing required fields.
With strict: true, functions receive correctly-typed arguments every time.

### How It Works
1. Define tool's input_schema (JSON Schema)
2. Set strict: true as top-level property in tool definition
3. Tool input field strictly follows input_schema
4. Tool name is always valid (from provided tools or server tools)

### Guarantees
- Tool input strictly follows the input_schema
- Tool name is always valid

## Using Both Together
- JSON outputs control Claude's response format (what Claude says)
- Strict tool use validates tool parameters (how Claude calls functions)
- Can be combined in same request

## Supported JSON Schema Features
Standard JSON Schema with some limitations (additionalProperties: false required on objects).

## Key Pattern: output_config vs output_format
- output_format parameter has moved to output_config.format
- Old output_format continues working during transition period
