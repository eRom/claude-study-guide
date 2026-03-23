# Prompting Best Practices for Claude 4.x
Source: https://platform.claude.com/docs/en/docs/build-with-claude/prompt-engineering/claude-4-best-practices

Single reference for prompt engineering with Claude Opus 4.6, Sonnet 4.6, Haiku 4.5.

## General Principles

### Be Clear and Direct
- Show your prompt to a colleague with minimal context. If they'd be confused, Claude will be too.
- Be specific about desired output format and constraints.
- Use numbered lists or bullet points when order matters.
- "Create an analytics dashboard. Include as many relevant features as possible. Go beyond the basics."

### Add Context to Improve Performance
- Explain WHY behavior is important, not just WHAT.
- "Your response will be read aloud by TTS, so never use ellipses" > "NEVER use ellipses"

### Use Examples Effectively (Few-Shot)
- 3-5 examples for best results
- Make examples: Relevant, Diverse (cover edge cases), Structured (wrap in <example> tags)

### Structure Prompts with XML Tags
- Use consistent, descriptive tag names (<instructions>, <context>, <input>)
- Nest tags when content has natural hierarchy

### Give Claude a Role
- Even a single sentence makes a difference
- Set role in system prompt

### Long Context Prompting
- Put longform data at the TOP (above query/instructions/examples)
- Queries at the end improve quality by up to 30%
- Structure documents with <document> tags with index and source metadata
- Ground responses in quotes for long document tasks

## Output and Formatting

### Communication Style
- Claude 4.x: More direct, more conversational, less verbose
- May skip verbal summaries after tool calls
- Request "provide a quick summary" if you want visibility

### Control Response Format
1. Tell Claude what to DO (not what NOT to do)
2. Use XML format indicators
3. Match your prompt style to desired output
4. Use detailed prompts for specific formatting

### LaTeX Output
- Opus 4.6 defaults to LaTeX for math
- Add explicit "Format in plain text only" to override

### Migrating Away from Prefilled Responses
- No longer supported on Claude 4.6+
- Use Structured Outputs instead of JSON prefills
- Use direct instructions instead of preamble prefills
- Move continuations to user message

## Tool Use

### Explicit Action Instructions
- "Can you suggest changes" -> Claude only suggests
- "Change this function" -> Claude takes action
- Add <default_to_action> or <do_not_act_before_instructions> to system prompt

### Optimize Parallel Tool Calling
- Claude 4.x excels at parallel tool execution
- Add <use_parallel_tool_calls> prompt for ~100% success rate
- "Make all independent calls in parallel"

## Thinking and Reasoning

### Overthinking Prevention
- Replace blanket defaults with targeted instructions
- Remove over-prompting (tools that undertriggered before trigger appropriately now)
- Use effort parameter as fallback

### Adaptive Thinking
- Claude Opus 4.6: adaptive thinking (thinking: {type: "adaptive"})
- Claude calibrates based on effort parameter + query complexity
- Adaptive thinking reliably drives better performance than extended thinking

### Guidance
- "Prefer general instructions over prescriptive steps"
- Multishot examples work with thinking (use <thinking> tags in few-shot)
- Ask Claude to self-check before finishing

## Agentic Systems

### Long-Horizon Reasoning
- Exceptional state tracking across extended sessions
- Context awareness: model tracks remaining context window

### Multi-Context Window Workflows
1. Use different prompt for first context window (setup framework)
2. Have model write tests in structured format (tests.json)
3. Set up quality-of-life tools (init.sh)
4. Consider fresh start vs compaction
5. Provide verification tools (Playwright MCP, computer use)

### State Management
- Structured formats (JSON) for state data
- Unstructured text for progress notes
- Git for state tracking and checkpoints
- Emphasize incremental progress

### Balancing Autonomy and Safety
- Prompt for confirmation before risky/irreversible actions
- Delete, force-push, posting to external services = confirm first

### Subagent Orchestration
- Claude 4.x: significantly improved native subagent orchestration
- May overuse subagents; add guidance on when to use direct approach
- "Use subagents when tasks can run in parallel, require isolated context"

### Avoid Hard-Coding
- "Write a general-purpose solution, not one that only works for test cases"
- "If tests are incorrect, inform me rather than working around them"

### Minimize Hallucinations
- "Never speculate about code you have not opened"
- "Read relevant files BEFORE answering questions about the codebase"

## Migration to Claude 4.6
1. Be specific about desired behavior
2. Frame instructions with modifiers
3. Request features explicitly
4. Update thinking config to adaptive
5. Migrate away from prefilled responses
6. Tune anti-laziness prompting (dial back aggressive language)
