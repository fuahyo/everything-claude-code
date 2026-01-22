---
description: Reviews code for quality, security, and maintainability before committing. Invokes code-reviewer agent to analyze uncommitted changes and provide actionable feedback.
---

# Code Review Command

This command invokes the **code-reviewer** agent to perform comprehensive security and quality review of uncommitted changes.

## What This Command Does

1. **Analyzes uncommitted changes** - Uses `git diff` to identify modified files
2. **Security vulnerability detection** - Checks for OWASP Top 10 and common security issues
3. **Code quality review** - Evaluates maintainability, readability, and best practices
4. **Provides actionable feedback** - Suggests specific fixes with severity levels
5. **Blocks unsafe commits** - Prevents committing code with critical issues

## When to Use

Use `/code-review` when:
- Before committing code changes
- After writing new features
- During pull request preparation
- After refactoring code
- When reviewing someone else's code

## When NOT to Use

- For documentation-only changes
- When code is still in active development (incomplete)
- For simple formatting changes
- When you've already reviewed the code manually

## How It Works

The code-reviewer agent will:

1. **Get changed files**: `git diff --name-only HEAD`
2. **Analyze each file** for issues in these categories:

### Security Issues (CRITICAL)
- Hardcoded credentials, API keys, tokens
- SQL injection vulnerabilities
- XSS vulnerabilities
- Missing input validation
- Insecure dependencies
- Path traversal risks
- CSRF vulnerabilities
- Authentication bypasses

### Code Quality (HIGH)
- Functions > 50 lines
- Files > 800 lines
- Nesting depth > 4 levels
- Missing error handling
- console.log statements
- TODO/FIXME comments without tickets
- Missing JSDoc for public APIs

### Best Practices (MEDIUM)
- Mutation patterns (use immutable instead)
- Emoji usage in code/comments
- Missing tests for new code
- Accessibility issues (a11y)
- Poor variable naming
- Magic numbers without explanation

3. **Generate report** with:
   - Severity: CRITICAL, HIGH, MEDIUM, LOW
   - File location and line numbers
   - Issue description
   - Suggested fix with code examples

4. **Block commit** if CRITICAL or HIGH issues found

## Example Usage

```
User: /code-review

Agent (code-reviewer):
# Code Review Report

## Summary
- Files reviewed: 3
- Critical issues: 1
- High issues: 2
- Medium issues: 5
- Recommendation: ❌ BLOCK - Fix critical issues before committing

## Critical Issues

### 1. Hardcoded API Key
**File:** `src/api/client.ts:42`
**Issue:** API key exposed in source code
**Fix:** Move to environment variable

```typescript
// ❌ Bad
const apiKey = "sk-proj-xxxxx"

// ✅ Good
const apiKey = process.env.OPENAI_API_KEY
if (!apiKey) {
  throw new Error('OPENAI_API_KEY not configured')
}
```

## High Issues

### 2. Missing Error Handling
**File:** `src/lib/utils.ts:15`
**Issue:** Function doesn't handle null input
**Fix:** Add null check and error handling
...
```

## Integration

This command invokes the `code-reviewer` agent located at:
`~/.claude/agents/code-reviewer.md`

The agent uses tools: Read, Grep, Glob, Bash

## Related Commands

- `/build-fix` - Fix build errors before review
- `/tdd` - Ensure tests are written before review
- `/test-coverage` - Verify coverage requirements
- `/security-review` - Deep security analysis (if available)

## Important Notes

**CRITICAL**: Never approve code with security vulnerabilities!

The review focuses on:
- Security (highest priority)
- Code quality and maintainability
- Best practices and conventions
- Test coverage for new code

All critical and high issues must be resolved before committing.
