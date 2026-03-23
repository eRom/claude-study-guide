# Skill Authoring Best Practices
Source: https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices

## Core Principles

### Concise is Key
- Context window is a public good shared with system prompt, history, other skills
- Only metadata (name + description) pre-loaded at startup
- SKILL.md loaded when relevant, additional files on demand
- Default: Claude is already very smart — only add what it doesn't know

### Set Appropriate Degrees of Freedom
- **High freedom** (text instructions): multiple valid approaches, context-dependent
- **Medium freedom** (pseudocode/parameterized scripts): preferred pattern exists, some variation OK
- **Low freedom** (exact scripts): fragile operations, consistency critical, exact sequence required
- Analogy: narrow bridge (low freedom) vs open field (high freedom)

### Test with All Models
- Haiku: needs more guidance?
- Sonnet: clear and efficient?
- Opus: avoid over-explaining?

## Skill Structure

### YAML Frontmatter
- `name`: max 64 chars, lowercase + hyphens, no "anthropic"/"claude"
- `description`: max 1024 chars, non-empty, no XML tags
- Description = discovery mechanism (Claude uses it to choose from 100+ skills)

### Naming: Use Gerund Form
- Good: `processing-pdfs`, `analyzing-spreadsheets`, `testing-code`
- Avoid: `helper`, `utils`, `tools` (vague)

### Description: Always Third Person
- Good: "Processes Excel files and generates reports"
- Bad: "I can help you..." or "You can use this to..."
- Include WHAT it does + WHEN to use it + trigger terms

### Progressive Disclosure (3 patterns)

**Pattern 1: High-level guide + references**
```
SKILL.md (overview + quick start)
├── FORMS.md (loaded when needed)
├── REFERENCE.md (loaded when needed)
└── EXAMPLES.md (loaded when needed)
```

**Pattern 2: Domain-specific organization**
```
bigquery-skill/
├── SKILL.md (overview + navigation)
└── reference/
    ├── finance.md, sales.md, product.md, marketing.md
```

**Pattern 3: Conditional details**
- Basic content in SKILL.md
- Advanced features in separate files, loaded only when needed

### Keep References ONE Level Deep
- Bad: SKILL.md -> advanced.md -> details.md (too deep, partial reads)
- Good: SKILL.md -> advanced.md, reference.md, examples.md (all direct)

### Token Budget
- SKILL.md body under 500 lines
- Longer? Split into separate files

## Workflows & Feedback Loops

### Checklist Pattern
- Provide copyable checklist for multi-step tasks
- Claude can track progress through complex workflows

### Feedback Loop Pattern
- Run validator -> fix errors -> repeat
- Catches errors early, provides objective verification

## Evaluation-Driven Development
1. Run Claude WITHOUT skill, document failures
2. Create 3 evaluation scenarios
3. Establish baseline performance
4. Write minimal instructions to address gaps
5. Iterate: evaluate, compare, refine

## Iterative Development with Claude
- **Claude A** (expert): designs/refines the skill
- **Claude B** (agent): tests skill in real tasks
- Observe B's behavior -> bring insights back to A -> refine -> retest

## Anti-Patterns
- Windows-style paths (use forward slashes always)
- Too many options (provide one default + escape hatch)
- Deeply nested references
- Assuming tools are installed
- Time-sensitive information
- Vague descriptions

## Executable Scripts in Skills
- Pre-made scripts > generated code (more reliable, save tokens)
- Handle errors explicitly in scripts (don't punt to Claude)
- No "voodoo constants" — document all magic numbers
- "plan-validate-execute" pattern for complex operations
- MCP tools: always use fully qualified names (ServerName:tool_name)

## Checklist Before Sharing
- [ ] Specific description with trigger terms
- [ ] Under 500 lines
- [ ] One-level-deep references
- [ ] No time-sensitive info
- [ ] Consistent terminology
- [ ] Tested with Haiku, Sonnet, Opus
- [ ] 3+ evaluation scenarios
- [ ] Scripts handle errors explicitly
