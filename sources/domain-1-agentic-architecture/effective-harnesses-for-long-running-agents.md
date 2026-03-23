# Effective Harnesses for Long-Running Agents
Source: https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents
Published: November 26, 2025

## Core Problem
Each new session begins with no memory of what came before. Two main failure patterns:
1. **Over-ambition**: Attempting to complete entire applications in single sessions
2. **Premature completion**: Declaring projects finished after partial progress

## Proposed Solution: Two-Component System

### Initializer Agent
Sets up the foundational environment:
- init.sh script for running development servers
- claude-progress.txt file documenting prior work
- Initial git commit establishing baseline state

### Coding Agent
Handles subsequent sessions:
- Reading progress files and git history
- Working on single features incrementally
- Leaving clean, well-documented code states

## Key Implementation Details
- **Feature List Management**: JSON file with granular feature requirements (200+), initially marked as "failing"
- **Testing Protocol**: End-to-end browser automation (Puppeteer MCP) rather than just unit tests
- **Session Startup Routine**: Check working dir, review progress docs, select next-priority features, verify existing functionality before implementing new ones
