# Contexts

Dynamic system prompt injection contexts that modify Claude's behavior based on the current mode or task type.

## Purpose

Contexts are mode-specific configurations that:
- **Modify behavior** - Change how Claude approaches tasks
- **Optimize for mode** - Tailor responses to current activity
- **Set priorities** - Focus on different aspects (speed vs. quality)
- **Guide tool usage** - Suggest which tools to favor

## When to Use

Contexts are typically:
- **Automatically activated** - Based on detected task type or user intent
- **Manually set** - Via configuration or explicit mode switching
- **Project-specific** - Defined per project in `CLAUDE.md`

## When NOT to Use

- For general tasks where default behavior is sufficient
- When you want consistent behavior across all tasks
- For simple, straightforward operations

## Available Contexts

### dev.md
**Purpose:** Active development mode - prioritize working solutions.

**Behavior:**
- Write code first, explain after
- Prefer working solutions over perfect solutions
- Run tests after changes
- Keep commits atomic

**Priorities:**
1. Get it working
2. Get it right
3. Get it clean

**Tools to favor:**
- Edit, Write for code changes
- Bash for running tests/builds
- Grep, Glob for finding code

**When to use:**
- Actively coding features
- Implementing planned work
- Fixing bugs
- Building functionality

**Location:** `contexts/dev.md`

---

### research.md
**Purpose:** Exploration and investigation mode - understand before acting.

**Behavior:**
- Read widely before concluding
- Ask clarifying questions
- Document findings as you go
- Don't write code until understanding is clear

**Research Process:**
1. Understand the question
2. Explore relevant code/docs
3. Form hypothesis
4. Verify with evidence
5. Summarize findings

**Tools to favor:**
- Read for understanding code
- Grep, Glob for finding patterns
- WebSearch, WebFetch for external docs
- Task with Explore agent for codebase questions

**Output:**
Findings first, recommendations second

**When to use:**
- Investigating bugs or issues
- Learning new codebases
- Researching solutions
- Understanding requirements

**Location:** `contexts/research.md`

---

### review.md
**Purpose:** Code review mode - focus on quality and security.

**Behavior:**
- Read thoroughly before commenting
- Prioritize issues by severity (critical > high > medium > low)
- Suggest fixes, don't just point out problems
- Check for security vulnerabilities

**Review Checklist:**
- [ ] Logic errors
- [ ] Edge cases
- [ ] Error handling
- [ ] Security (injection, auth, secrets)
- [ ] Performance
- [ ] Readability
- [ ] Test coverage

**Output Format:**
Group findings by file, severity first

**When to use:**
- Reviewing pull requests
- Code quality audits
- Security reviews
- Pre-commit reviews

**Location:** `contexts/review.md`

---

## Context Structure

Contexts are simple markdown files that define behavior:

```markdown
# Context Name

Mode: [mode description]
Focus: [what to focus on]

## Behavior
- [behavioral guideline 1]
- [behavioral guideline 2]

## Priorities
1. [priority 1]
2. [priority 2]

## Tools to favor
- [tool 1] - [when to use]
- [tool 2] - [when to use]
```

## Context Activation

Contexts can be activated through:

1. **Project configuration** - Set in `CLAUDE.md`:
   ```markdown
   ---
   context: dev
   ---
   ```

2. **Automatic detection** - Based on task type or commands

3. **Manual switching** - User explicitly requests mode change

## Creating Custom Contexts

You can create project-specific contexts:

1. Create a new markdown file in `contexts/`
2. Define behavior, priorities, and tool preferences
3. Reference in project `CLAUDE.md`:
   ```markdown
   ---
   context: my-custom-context
   ---
   ```

## Best Practices

- **Use appropriate context** - Match context to task type
- **Let contexts guide behavior** - Trust the mode-specific guidance
- **Switch contexts when needed** - Don't force one context for all tasks
- **Keep contexts focused** - Each context should have a clear purpose

## Notes / Limitations

- Contexts modify behavior but don't override explicit instructions
- Contexts are suggestions, not hard rules
- Some contexts may conflict - use the most appropriate one
- Contexts work best when tasks clearly match their purpose

---

**See also:**
- [Main README](../README.md) - Overview of repository
- [Rules](../rules/) - Rules that may reference contexts
- [Examples](../examples/) - Example project configurations
