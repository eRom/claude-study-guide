# Claude Certified Architect — Foundations | Preparation Guide
Source: https://dynamicbalaji.medium.com/claude-certified-architect-foundations-certification-preparation-guide
Author: Balaji Ashok Kumar

## Exam Structure
- 5 domains + 6 scenario contexts
- 4 of the 6 scenarios randomly selected per exam
- All questions anchored to specific production scenarios
- Passing score: 720 on a 100-1,000 scale

## The 6 Exam Scenarios
1. Customer Support Resolution Agent
2. Code Generation with Claude Code
3. Multi-Agent Research System
4. Developer Productivity with Claude
5. Claude Code for CI/CD
6. Structured Data Extraction

## The 5 Mental Models That Actually Matter

### 1. Programmatic enforcement vs. prompt-based guidance
THE single most tested concept. When something MUST happen (identity verification before refund, blocking tool call above threshold) -> use programmatic enforcement: hooks, prerequisite gates, tool-call interceptors.
"Prompts are probabilistic. For compliance-critical workflows, a non-zero failure rate is unacceptable."

### 2. Tool descriptions are the PRIMARY routing mechanism
Not the system prompt. Not the function name. The DESCRIPTION. Fix overlapping tools by writing descriptions that include input formats, example queries, edge cases, and explicit boundaries.

### 3. Subagents don't inherit context — EVER
Every piece of information a subagent needs must be explicitly passed in its prompt. No shared memory, no automatic history propagation.

### 4. The "lost in the middle" effect is a real design constraint
Models reliably process content at beginning and end, but middle gets missed. Place key summaries at top, use explicit section headers, trim verbose tool outputs.

### 5. Batch API vs. real-time is a LATENCY decision, not a cost decision
Batch API: 50% cost savings, up to 24h processing, no guaranteed SLA. Blocking workflows MUST use real-time API.

## Common Traps

| Trap (Wrong Answer) | Why It's Wrong |
|---|---|
| Add few-shot examples to enforce tool ordering | Ordering is compliance -> use programmatic prerequisites |
| Self-reported confidence scores for escalation | LLM confidence is poorly calibrated |
| Route all workflows to batch API for cost savings | Batch has no SLA, blocking workflows need real-time |
| A larger context window fixes attention dilution | Context size != attention quality, split into focused passes |
| Return empty results on subagent failure | Silently suppresses errors, prevents recovery |
| Give all agents access to all tools | 18 tools degrades selection, scope to 4-5 per agent |

## DOMAIN 1 — Agentic Architecture & Orchestration (27%)

### 1.1 Agentic Loop
- Continue when stop_reason = "tool_use"
- Terminate when stop_reason = "end_turn"
- Append tool results to conversation history between every iteration
- ANTI-PATTERNS: Parse natural language to detect loop end, arbitrary iteration cap, check assistant text

### 1.2 Multi-Agent Hub-and-Spoke
- Coordinator manages ALL inter-subagent communication, error handling, routing
- Subagents have ISOLATED context (no inheritance)
- Route ALL communication through coordinator
- Use iterative refinement: evaluate synthesis -> re-delegate gaps -> re-synthesise

### 1.3 Subagent Context Passing
- Task tool spawns subagents; allowedTools must include "Task"
- Pass complete findings explicitly in subagent's prompt
- Use structured data to separate content from metadata
- Spawn parallel subagents via multiple Task calls in single response
- Use fork_session for divergent approaches

### 1.4 Enforcement & Handoffs
- Block process_refund until get_customer returns verified customer ID
- Handoff summary: customer ID, root cause, refund amount, recommended action

### 1.5 Hooks
- PostToolUse: normalise heterogeneous formats before model processes them
- Tool call interception: block policy violations (refunds > $500) -> redirect to escalation
- Hooks = deterministic guarantees; Prompts = probabilistic compliance

### 1.6 Task Decomposition
- Prompt chaining = predictable fixed sequential steps
- Dynamic decomposition = open-ended investigation
- Large code reviews: per-file local pass + separate cross-file integration pass

### 1.7 Session Management
- --resume <session-name> continues prior session
- fork_session creates independent branches
- Fresh session + structured summary > resuming with stale tool results

## DOMAIN 2 — Tool Design & MCP Integration (18%)

### 2.1 Tool Description Design
- Include: input formats, example queries, edge cases, explicit boundaries vs similar tools
- Rename to eliminate overlap: analyze_content -> extract_web_results
- Split generic tools into purpose-specific tools

### 2.2 Structured Error Responses
- Transient (timeout) -> isRetryable: true
- Validation (invalid input) -> isRetryable: false
- Business (policy violation) -> isRetryable: false
- Distinguish access failure from valid empty result

### 2.3 Tool Distribution & tool_choice
- Target 4-5 tools per agent, NOT 18
- "auto" = may return text instead of tool call
- "any" = must call a tool, model chooses which
- {"type": "tool", "name": "..."} = forced specific tool

### 2.4 MCP Server Configuration
- .mcp.json = project-level, shared via VCS
- ~/.claude.json = user-level, personal
- Use ${GITHUB_TOKEN} env var expansion, never commit secrets
- MCP Resources expose content catalogs to reduce exploratory tool calls

### 2.5 Built-in Tools
- Grep = search file contents for patterns
- Glob = match file paths by pattern
- Edit = targeted modifications using unique text matching
- Build understanding incrementally: Grep entry points -> Read imports

## DOMAIN 3 — Claude Code Configuration & Workflows (20%)

### 3.1 CLAUDE.md Hierarchy
- ~/.claude/CLAUDE.md = user only, NOT shared with team
- .claude/CLAUDE.md = project-level, version-controlled, team-wide
- Subdirectory CLAUDE.md = scoped to that directory
- Use @import for modularity
- Use .claude/rules/ for topic-specific rules
- Use /memory to verify loaded files

### 3.2 Slash Commands & Skills
- .claude/commands/ = project, shared via VCS
- ~/.claude/commands/ = personal, not shared
- Skills frontmatter: context: fork (isolated sub-agent), allowed-tools, argument-hint
- Skills = on-demand; CLAUDE.md = always-loaded

### 3.3 Path-Specific Rules
- .claude/rules/ with YAML paths field + glob patterns
- Loads only when editing matching files
- Better than subdirectory CLAUDE.md for cross-directory conventions

### 3.4 Plan Mode vs Direct Execution
- Plan Mode: large-scale changes, multiple approaches, architectural decisions
- Direct: single-file, clear stack trace, simple additions
- Best pattern: Plan mode to investigate -> Direct execution to implement

### 3.5 Iterative Refinement
- 2-3 concrete I/O examples when prose is inconsistent
- Test-driven: write tests first, share failures
- Interacting issues -> one message; Independent -> sequential

### 3.6 CI/CD Integration
- -p (--print) flag for non-interactive mode
- --output-format json + --json-schema for structured PR comments
- Independent session for review (don't review your own code)

## DOMAIN 4 — Prompt Engineering & Structured Output (20%)

### 4.1 Explicit Criteria
- "Flag comments only when claimed behaviour contradicts actual code" > "Check that comments are accurate"
- High false-positive categories undermine trust in ALL categories

### 4.2 Few-Shot Prompting
- Most effective technique for consistent formatting
- 2-4 targeted examples for ambiguous scenarios
- Show reasoning behind the choice
- Include acceptable patterns alongside genuine issues

### 4.3 Structured Output via tool_use
- JSON schemas eliminate syntax errors, NOT semantic errors
- Nullable fields for optional info (prevents fabrication)
- "unclear" enum values for ambiguous cases
- "other" + detail string for extensible categorisation
- tool_choice: "any" for unknown document types

### 4.4 Validation & Retry Loops
- On failure: send original document + failed extraction + specific validation errors
- Retries work for: format mismatches, structural errors
- Retries DON'T work for: absent information

### 4.5 Batch Processing
- 50% cost savings, up to 24h, no SLA, no multi-turn tool calling
- custom_id for request/response correlation
- Synchronous API -> blocking pre-merge checks, live interactions
- Batches -> overnight reports, weekly audits

### 4.6 Multi-Instance Review
- Model retains reasoning context, less likely to question own decisions
- Use SECOND independent instance to review generated code
- Split large reviews: per-file + separate cross-file pass

## DOMAIN 5 — Context Management & Reliability (15%)

### 5.1 Long Conversation Context
- Extract transactional facts into persistent "case facts" block
- Trim verbose tool outputs (40+ fields -> 5 relevant)
- Place key findings at beginning
- Always pass complete conversation history

### 5.2 Escalation Patterns
- Customer requests human -> escalate immediately
- Policy gap -> escalate
- Frustrated but straightforward -> acknowledge, offer resolution first
- Self-reported confidence = unreliable routing signal
- Multiple customer matches -> ask for identifiers, don't select by heuristic

### 5.3 Error Propagation in Multi-Agent
- Return: failure type, what was attempted, partial results, alternatives
- NEVER return empty results as success
- NEVER terminate entire workflow on single subagent failure
- Subagents: local recovery for transient; propagate unresolvable + partial results

### 5.4 Large Codebase Context
- Scratchpad files for key findings
- Spawn subagents for specific questions
- Summarise before spawning next phase
- Crash recovery: export state to manifest, load on resume
- /compact for extended exploration

### 5.5 Human Review & Confidence
- 97% overall can mask poor performance on specific types
- Stratified random sampling of high-confidence extractions
- Analyse accuracy by document type AND by field

### 5.6 Information Provenance
- Require structured claim-source mappings
- When sources conflict: annotate both with source attribution
- Include publication dates
- Distinguish well-established vs contested findings

## Key Facts to Memorize

| Fact | Value |
|---|---|
| Passing score | 720 / 1000 |
| Batch API savings | 50% cost |
| Batch API SLA | None (up to 24h) |
| tool_choice "auto" | May return text |
| tool_choice "any" | Must call a tool |
| stop_reason "tool_use" | Continue loop |
| stop_reason "end_turn" | Terminate |
| CLAUDE.md user | ~/.claude/CLAUDE.md (NOT shared) |
| CLAUDE.md project | .claude/CLAUDE.md (team-wide) |
| MCP project config | .mcp.json (shared VCS) |
| MCP user config | ~/.claude.json (personal) |
| CI/CD flag | -p (--print) non-interactive |
| context: fork | Skill runs in isolated sub-agent |

## Official Exam Guide PDF
https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2F8lsy243ftffjjy1cx9lm3o2bw%2Fpublic%2F1773274827%2FClaude+Certified+Architect+%E2%80%93+Foundations+Certification+Exam+Guide.pdf
