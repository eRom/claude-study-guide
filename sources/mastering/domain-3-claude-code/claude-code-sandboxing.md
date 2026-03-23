# Beyond Permission Prompts: Making Claude Code More Secure and Autonomous
Source: https://www.anthropic.com/engineering/claude-code-sandboxing
Published: October 20, 2025

## Problem
- Permission-based model causes "approval fatigue"
- Users stop carefully reviewing approvals -> paradoxically reduces security

## Solution: Sandboxing
Predefined boundaries enabling Claude to work freely without per-action permission.

### Two Critical Components (BOTH needed)
1. **Filesystem isolation** — restricts access to specific directories
2. **Network isolation** — limits connections to approved servers

Without network isolation: compromised agents can steal SSH keys.
Without filesystem isolation: sandbox escape possible.

## Two New Features

### Sandboxed Bash Tool
- OS-level primitives: Linux bubblewrap, macOS seatbelt
- Read/write to current working directory only
- Network via Unix domain socket to proxy server
- Proxy enforces domain restrictions
- Even successful prompt injection remains isolated

### Claude Code on the Web
- Isolated cloud sandboxes with full server access
- Credentials (git, signing keys) remain OUTSIDE sandbox
- Custom proxy for git with scoped credentials
- Branch-level restrictions possible

## Key Insight
Sandboxing reduced permission prompts by 84% while enhancing security.
