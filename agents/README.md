# Agents

Specialized subagents for task delegation and focused problem-solving. Each agent has a specific domain expertise and is invoked automatically or manually to handle particular types of tasks.

## Purpose

Agents are specialized Claude Code configurations that focus on specific problem domains. They enable:
- **Focused expertise** - Each agent is optimized for its domain
- **Task delegation** - Main Claude can delegate to specialized agents
- **Consistent patterns** - Agents enforce best practices in their domains
- **Efficiency** - Agents use appropriate tools and models for their tasks

## When to Use

Agents are typically invoked:
- **Automatically** - When rules detect a task matching an agent's domain
- **Manually** - Via commands like `/plan`, `/tdd`, `/code-review`
- **By delegation** - When the main Claude determines a task needs specialized expertise

## When NOT to Use

- For simple, straightforward tasks that don't need specialized knowledge
- When the main Claude can handle the task directly
- For tasks that span multiple domains (use planner first, then delegate)

## Available Agents

### planner
**Purpose:** Creates comprehensive implementation plans for complex features and refactorings.

**When to use:**
- Starting new features
- Planning architectural changes
- Complex refactoring tasks
- Multi-file implementations

**When NOT to use:**
- Simple bug fixes
- Single-file changes
- Tasks with clear, straightforward requirements

**Example usage:**
```
User: I need to add real-time notifications
Agent: Creates detailed plan with phases, dependencies, and risks
```

**Location:** `agents/planner.md`

---

### architect
**Purpose:** Designs system architecture, evaluates technical trade-offs, and makes architectural decisions.

**When to use:**
- Designing new systems or major features
- Evaluating technology choices
- Planning scalability improvements
- Making architectural decisions

**When NOT to use:**
- Implementation details
- Simple feature additions
- Bug fixes

**Example usage:**
```
User: Should we use Redis or PostgreSQL for caching?
Agent: Evaluates trade-offs, recommends approach with ADR
```

**Location:** `agents/architect.md`

---

### tdd-guide
**Purpose:** Enforces test-driven development methodology with 80%+ coverage.

**When to use:**
- Writing new features
- Fixing bugs (write test first)
- Refactoring code
- Building critical business logic

**When NOT to use:**
- Documentation-only changes
- Configuration updates
- Simple formatting changes

**Example usage:**
```
User: Add a function to calculate market liquidity
Agent: Writes failing test first, then implements minimal code
```

**Location:** `agents/tdd-guide.md`

---

### code-reviewer
**Purpose:** Reviews code for quality, security, and maintainability.

**When to use:**
- After writing or modifying code
- Before committing changes
- During pull request reviews
- When refactoring

**When NOT to use:**
- For planning tasks
- For documentation-only changes

**Example usage:**
```
User: Review my recent changes
Agent: Analyzes code, flags issues by severity, suggests fixes
```

**Location:** `agents/code-reviewer.md`

---

### security-reviewer
**Purpose:** Detects security vulnerabilities and enforces security best practices.

**When to use:**
- After writing code that handles user input
- Creating new API endpoints
- Implementing authentication/authorization
- Working with sensitive data
- Before production deployments

**When NOT to use:**
- For non-security code reviews
- Documentation updates

**Example usage:**
```
User: Review this authentication code
Agent: Checks for OWASP Top 10, secrets exposure, injection risks
```

**Location:** `agents/security-reviewer.md`

---

### build-error-resolver
**Purpose:** Fixes TypeScript and build errors quickly with minimal changes.

**When to use:**
- Build failures
- TypeScript errors
- Compilation errors
- Import/module resolution issues

**When NOT to use:**
- For refactoring (use refactor-cleaner)
- For architectural changes (use architect)
- When build is passing

**Example usage:**
```
User: Build is failing with type errors
Agent: Fixes type errors with minimal diffs, gets build green
```

**Location:** `agents/build-error-resolver.md`

---

### e2e-runner
**Purpose:** Generates, maintains, and runs end-to-end tests with Playwright.

**When to use:**
- Testing critical user journeys
- Verifying multi-step flows
- Preparing for production deployment
- Validating UI interactions

**When NOT to use:**
- For unit tests (use tdd-guide)
- For simple component tests
- When E2E tests already exist and pass

**Example usage:**
```
User: Test the market search and view flow
Agent: Generates Playwright test, runs it, captures artifacts
```

**Location:** `agents/e2e-runner.md`

---

### refactor-cleaner
**Purpose:** Removes dead code, eliminates duplicates, and cleans up codebase.

**When to use:**
- Removing unused code
- Consolidating duplicates
- Cleaning up dependencies
- Codebase maintenance

**When NOT to use:**
- During active feature development
- Right before production deployment
- When codebase is unstable
- Without proper test coverage

**Example usage:**
```
User: Clean up unused code
Agent: Runs knip/depcheck, safely removes dead code, documents deletions
```

**Location:** `agents/refactor-cleaner.md`

---

### doc-updater
**Purpose:** Updates codemaps and documentation to reflect current codebase state.

**When to use:**
- After major features added
- When architecture changes
- Before releases
- When documentation is outdated

**When NOT to use:**
- For minor bug fixes
- When code hasn't changed significantly

**Example usage:**
```
User: Update documentation
Agent: Regenerates codemaps, updates READMEs, verifies links
```

**Location:** `agents/doc-updater.md`

---

## Agent Configuration

Each agent file follows this structure:

```markdown
---
name: agent-name
description: Brief description of what this agent does
tools: Read, Write, Edit, Bash, Grep, Glob
model: opus
---

# Agent Title

[Agent documentation with purpose, workflow, examples]
```

## Agent Invocation

Agents are invoked through:
1. **Commands** - `/plan`, `/tdd`, `/code-review`, etc.
2. **Rules** - Automatic detection based on task type
3. **Manual delegation** - Main Claude decides to use an agent

## Best Practices

- **One agent per task** - Don't chain multiple agents unnecessarily
- **Let agents complete** - Don't interrupt agent workflows
- **Review agent output** - Agents provide recommendations, verify them
- **Use appropriate agent** - Match agent to task domain

## Notes / Limitations

- Agents operate independently - they don't share context automatically
- Some agents require specific tools (e.g., e2e-runner needs Playwright)
- Agent recommendations should be reviewed before implementation
- Agents follow their own rules and may not be aware of project-specific constraints

---

**See also:**
- [Commands](../commands/README.md) - Commands that invoke agents
- [Rules](../rules/agents.md) - Rules for agent delegation
- [Main README](../README.md) - Overview of entire repository
