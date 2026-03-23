# Demystifying Evals for AI Agents
Source: https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents

## Key Definitions
- **Task**: Single test with defined inputs and success criteria
- **Trial**: Each attempt at a task (multiple runs for consistency)
- **Grader**: Logic scoring agent performance (code-based, model-based, human)
- **Transcript**: Complete record of a trial (messages, tool calls, reasoning)
- **Outcome**: Final state in environment (not just what agent says)
- **Eval harness**: Infrastructure running evals end-to-end
- **Agent harness**: System enabling model to act as agent

## Types of Graders

### Code-Based (fast, cheap, objective)
- String match, regex, binary tests (fail-to-pass)
- Static analysis (lint, type, security)
- Outcome verification, tool calls verification

### Model-Based (flexible, handles nuance)
- Rubric-based scoring, natural language assertions
- Pairwise comparison, multi-judge consensus
- Requires calibration with human graders

### Human (gold standard)
- SME review, crowdsourced judgment, A/B testing

## Capability vs Regression Evals
- **Capability**: "What can this agent do?" — start at low pass rate, hill to climb
- **Regression**: "Does it still work?" — should be ~100% pass rate

## Non-Determinism: pass@k vs pass^k
- **pass@k**: probability of at least one success in k attempts (rises with k)
- **pass^k**: probability of ALL k trials succeeding (falls with k)

## Roadmap: Zero to Great Evals
1. Start early (20-50 tasks from real failures)
2. Write unambiguous tasks with reference solutions
3. Build balanced problem sets (test both positive and negative cases)
4. Build robust eval harness with isolated environments
5. Design graders thoughtfully (grade outcomes, not paths)
6. Check the transcripts
7. Monitor for eval saturation
8. Keep evaluation suites healthy through open contribution

## By Agent Type
- **Coding agents**: Unit tests + LLM rubric for code quality
- **Conversational agents**: LLM rubric + state checks + tool call verification
- **Research agents**: Groundedness + coverage + source quality checks
- **Computer use agents**: URL/page state + backend verification
