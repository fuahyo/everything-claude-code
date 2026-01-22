# Commands

Slash commands for quick execution of common workflows. Commands provide a fast way to invoke agents and standardized processes.

## Purpose

Commands are user-invocable shortcuts that:
- **Invoke agents** - Trigger specialized agents for specific tasks
- **Standardize workflows** - Ensure consistent processes across sessions
- **Save time** - Quick access to common operations
- **Provide context** - Commands set up the right context for tasks

## When to Use

Use commands when:
- You want to follow a specific workflow (e.g., TDD, planning)
- You need to invoke a specialized agent
- You want consistent, repeatable processes
- You're starting a new task that matches a command's purpose

## When NOT to Use

- For simple, one-off tasks that don't need a structured workflow
- When you can accomplish the task directly without a command
- For exploratory tasks where you're not sure what you need

## Available Commands

### /plan
**Purpose:** Creates comprehensive implementation plan before coding.

**What it does:**
- Restates requirements clearly
- Identifies risks and dependencies
- Breaks down into phases and steps
- **Waits for confirmation** before proceeding

**When to use:**
- Starting new features
- Complex refactoring
- Architectural changes
- Multi-file implementations

**Example:**
```
/plan I need to add real-time notifications when markets resolve
```

**Invokes:** `planner` agent

**Location:** `commands/plan.md`

---

### /tdd
**Purpose:** Enforces test-driven development workflow.

**What it does:**
- Scaffolds interfaces first
- Writes failing tests (RED)
- Implements minimal code (GREEN)
- Refactors (IMPROVE)
- Verifies 80%+ coverage

**When to use:**
- Implementing new features
- Fixing bugs (test first)
- Refactoring code
- Building critical logic

**Example:**
```
/tdd Add a function to calculate market liquidity score
```

**Invokes:** `tdd-guide` agent

**Location:** `commands/tdd.md`

---

### /e2e
**Purpose:** Generates and runs end-to-end tests with Playwright.

**What it does:**
- Creates test journeys for user flows
- Runs tests across browsers
- Captures screenshots/videos/traces
- Identifies flaky tests

**When to use:**
- Testing critical user journeys
- Verifying multi-step flows
- Preparing for production
- Validating UI interactions

**Example:**
```
/e2e Test the market search and view flow
```

**Invokes:** `e2e-runner` agent

**Location:** `commands/e2e.md`

---

### /code-review
**Purpose:** Reviews code for quality, security, and maintainability.

**What it does:**
- Analyzes recent changes (git diff)
- Flags issues by severity
- Suggests specific fixes
- Provides approval recommendation

**When to use:**
- After writing code
- Before committing
- During PR reviews
- After refactoring

**Example:**
```
/code-review
```

**Invokes:** `code-reviewer` agent

**Location:** `commands/code-review.md`

---

### /build-fix
**Purpose:** Fixes build and TypeScript errors quickly.

**What it does:**
- Collects all build errors
- Fixes with minimal diffs
- Verifies build passes
- No architectural changes

**When to use:**
- Build failures
- TypeScript errors
- Compilation errors
- Import issues

**Example:**
```
/build-fix
```

**Invokes:** `build-error-resolver` agent

**Location:** `commands/build-fix.md`

---

### /refactor-clean
**Purpose:** Removes dead code and consolidates duplicates.

**What it does:**
- Runs detection tools (knip, depcheck)
- Safely removes unused code
- Consolidates duplicates
- Documents deletions

**When to use:**
- Codebase cleanup
- Removing unused code
- Consolidating duplicates
- Maintenance tasks

**Example:**
```
/refactor-clean
```

**Invokes:** `refactor-cleaner` agent

**Location:** `commands/refactor-clean.md`

---

### /update-docs
**Purpose:** Updates documentation and codemaps.

**What it does:**
- Regenerates codemaps from code
- Updates READMEs
- Verifies links
- Generates API reference

**When to use:**
- After major features
- When architecture changes
- Before releases
- When docs are outdated

**Example:**
```
/update-docs
```

**Invokes:** `doc-updater` agent

**Location:** `commands/update-docs.md`

---

### /update-codemaps
**Purpose:** Generates architectural codemaps from codebase.

**What it does:**
- Analyzes repository structure
- Maps modules and dependencies
- Generates codemap files
- Creates architecture diagrams

**When to use:**
- After structural changes
- When onboarding new developers
- Before major refactoring
- When architecture is unclear

**Example:**
```
/update-codemaps
```

**Invokes:** `doc-updater` agent (codemap generation)

**Location:** `commands/update-codemaps.md`

---

### /test-coverage
**Purpose:** Verifies test coverage meets 80%+ requirement.

**What it does:**
- Runs test coverage analysis
- Identifies uncovered code
- Suggests additional tests
- Generates coverage report

**When to use:**
- After implementing features
- Before committing
- During code review
- When coverage is low

**Example:**
```
/test-coverage
```

**Location:** `commands/test-coverage.md`

---

### /learn
**Purpose:** Extracts patterns from session into reusable skills.

**What it does:**
- Analyzes session for patterns
- Extracts reusable knowledge
- Creates skill files
- Documents learnings

**When to use:**
- After solving complex problems
- When discovering new patterns
- After workarounds or fixes
- When building reusable knowledge

**Example:**
```
/learn
```

**Location:** `commands/learn.md`

**Note:** This is an advanced feature from the Longform Guide.

---

## Command Structure

Commands are simple markdown files with frontmatter:

```markdown
---
description: Brief description of what this command does
---

# Command Name

[Detailed documentation]
```

## Command Execution Flow

1. **User invokes command** - `/command-name [optional context]`
2. **Command activates** - Sets up appropriate context
3. **Agent invoked** - Specialized agent handles the task
4. **Results provided** - Agent returns findings/recommendations
5. **User reviews** - User confirms or requests changes

## Best Practices

- **Use appropriate command** - Match command to task type
- **Provide context** - Give commands enough information
- **Review output** - Commands provide recommendations, verify them
- **Follow workflows** - Commands enforce best practices, follow them

## Integration with Agents

Most commands invoke specific agents:
- `/plan` → `planner` agent
- `/tdd` → `tdd-guide` agent
- `/e2e` → `e2e-runner` agent
- `/code-review` → `code-reviewer` agent
- `/build-fix` → `build-error-resolver` agent
- `/refactor-clean` → `refactor-cleaner` agent
- `/update-docs`, `/update-codemaps` → `doc-updater` agent

## Notes / Limitations

- Commands are synchronous - they complete before returning
- Some commands require specific tools (e.g., `/e2e` needs Playwright)
- Commands follow their workflows - they may not be flexible for edge cases
- Review command output before proceeding with recommendations

---

**See also:**
- [Agents](../agents/README.md) - Agents that commands invoke
- [Rules](../rules/) - Rules that may auto-invoke commands
- [Main README](../README.md) - Overview of entire repository
