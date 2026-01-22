# Development Context

Mode: Active development
Focus: Implementation, coding, building features

## Behavior
- Write code first, explain after
- Prefer working solutions over perfect solutions
- Run tests after changes
- Keep commits atomic
- Make incremental progress
- Don't over-engineer
- Focus on functionality over perfection

## Priorities
1. Get it working
2. Get it right
3. Get it clean

## Tools to favor
- Edit, Write for code changes
- Bash for running tests/builds
- Grep, Glob for finding code
- Read for understanding existing code quickly

## Example Scenarios

Use this context when:
- Implementing a planned feature
- Fixing bugs
- Adding new components
- Writing API endpoints
- Building functionality
- Following a TDD workflow

## When to Switch

Switch to `research.md` when:
- Requirements are unclear
- Need to understand existing codebase
- Exploring solutions or patterns
- Learning new technologies
- Investigating bugs

Switch to `review.md` when:
- Code is complete and needs review
- Preparing for commit
- Reviewing pull requests
- Quality assurance needed

## Tool Usage Patterns

**Code Changes:**
- Use `Edit` for small changes (< 50 lines)
- Use `Write` for new files
- Use `Bash` to run tests after changes
- Use `Grep` to find related code patterns

**Example Workflow:**
1. Read existing code to understand structure
2. Edit/Write code to implement feature
3. Run tests with Bash
4. Fix any issues
5. Commit when tests pass

## Integration

This context works well with:
- `/tdd` command - Test-driven development
- `/build-fix` command - Quick error resolution
- `planner` agent - For implementation planning
- `build-error-resolver` agent - Fix build errors quickly

## Related Files

- `contexts/research.md` - For exploration mode
- `contexts/review.md` - For review mode
- `README.md` - Overview of contexts
