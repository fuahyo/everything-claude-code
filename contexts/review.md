# Code Review Context

Mode: PR review, code analysis
Focus: Quality, security, maintainability

## Behavior
- Read thoroughly before commenting
- Prioritize issues by severity (critical > high > medium > low)
- Suggest fixes, don't just point out problems
- Check for security vulnerabilities
- Be constructive and helpful
- Focus on what matters most

## Review Checklist
- [ ] Logic errors
- [ ] Edge cases
- [ ] Error handling
- [ ] Security (injection, auth, secrets)
- [ ] Performance
- [ ] Readability
- [ ] Test coverage
- [ ] Code style consistency
- [ ] Documentation

## Example Scenarios

Use this context when:
- Reviewing pull requests
- Code quality audits
- Security reviews
- Pre-commit reviews
- Post-implementation review
- Quality assurance checks

## When to Switch

Switch to `dev.md` when:
- Review is complete
- Ready to implement fixes
- Need to make changes

Switch to `research.md` when:
- Need to understand code better
- Investigating issues found
- Researching best practices

## Tool Usage Patterns

**Review Process:**
- Use `Read` to understand code changes
- Use `Grep` to find related code
- Use `Bash` to run tests
- Use `Read` to check documentation

**Example Workflow:**
1. Read changed files completely
2. Check for security issues
3. Verify tests exist and pass
4. Review code quality
5. Provide prioritized feedback
6. Suggest specific fixes

## Output Format

Reviews should follow this structure:
```markdown
## Code Review Report

### Summary
- Critical: X
- High: Y
- Medium: Z
- Status: APPROVE / REQUEST CHANGES

### Critical Issues
[File:line] Issue description
Fix: [Suggested fix]

### High Issues
[Same format]

### Medium Issues
[Same format]

### Suggestions
[Optional improvements]
```

## Integration

This context works well with:
- `/code-review` command - Manual review
- `code-reviewer` agent - Automated review
- `security-reviewer` agent - Security-focused review

## Related Files

- `contexts/dev.md` - For implementation mode
- `contexts/research.md` - For exploration mode
- `agents/code-reviewer.md` - Review agent
- `README.md` - Overview of contexts
