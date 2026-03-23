# Agent Skills: Equipping AI Agents for Real-World Tasks
Source: https://claude.com/blog/equipping-agents-for-the-real-world-with-agent-skills

## Core Concept
Agent Skills = organized folders of instructions, scripts, and resources.
Like "onboarding guides for new hires" — package procedural knowledge into composable, reusable resources.

## Anatomy of a Skill
A skill is a directory containing a SKILL.md file with YAML frontmatter (name + description).

### Progressive Disclosure Design (3 levels)
1. **Level One**: Skill metadata (name + description) in system prompt at startup
2. **Level Two**: Full SKILL.md content loaded when Claude determines relevance
3. **Level Three+**: Additional bundled files referenced within SKILL.md, loaded on demand

## Context Window Management
1. Context window contains system prompt + skill metadata
2. Claude invokes a tool to read the full SKILL.md
3. Claude selectively loads additional referenced files
4. Agent proceeds with the task

## Code Execution
Skills can bundle executable code (Python scripts) that Claude runs directly — more efficient than token-based generation for deterministic operations.

## Development Guidelines
- Start with evaluation: identify capability gaps through testing
- Structure for scale: split unwieldy SKILL.md files
- Perspective-taking: monitor how Claude actually uses skills
- Iterative refinement: work with Claude to capture successful approaches

## Security
Install skills only from trusted sources. Audit all bundled files before use.
