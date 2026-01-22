# Research Context

Mode: Exploration, investigation, learning
Focus: Understanding before acting

## Behavior
- Read widely before concluding
- Ask clarifying questions
- Document findings as you go
- Don't write code until understanding is clear
- Explore multiple approaches
- Verify assumptions with evidence
- Summarize before recommending

## Research Process
1. Understand the question
2. Explore relevant code/docs
3. Form hypothesis
4. Verify with evidence
5. Summarize findings

## Tools to favor
- Read for understanding code
- Grep, Glob for finding patterns
- WebSearch, WebFetch for external docs
- Task with Explore agent for codebase questions
- Codebase search for semantic understanding

## Example Scenarios

Use this context when:
- Investigating bugs or issues
- Learning new codebases
- Researching solutions or patterns
- Understanding requirements
- Exploring technology options
- Analyzing existing implementations
- Before making architectural decisions

## When to Switch

Switch to `dev.md` when:
- Understanding is clear
- Ready to implement
- Have a clear plan
- Need to write code

Switch to `review.md` when:
- Research is complete
- Need to review findings
- Validating research results

## Tool Usage Patterns

**Exploration:**
- Use `Read` to understand code structure
- Use `Grep` to find patterns across codebase
- Use `Glob` to discover related files
- Use `CodebaseSearch` for semantic understanding

**Documentation:**
- Use `WebSearch` for external documentation
- Use `Read` for project documentation
- Document findings in markdown

**Example Workflow:**
1. Read relevant files to understand context
2. Search codebase for similar patterns
3. Research external documentation if needed
4. Form hypothesis about solution
5. Verify with code examples
6. Summarize findings and recommendations

## Output Format

Research should follow this structure:
```markdown
## Research Findings

### Question
[What we're trying to understand]

### Exploration
[What was explored]

### Findings
[Key discoveries]

### Hypothesis
[Proposed understanding]

### Evidence
[Code examples, documentation references]

### Recommendations
[Suggested next steps]
```

## Integration

This context works well with:
- `planner` agent - For planning after research
- `architect` agent - For architectural research
- `/plan` command - Planning based on research

## Related Files

- `contexts/dev.md` - For implementation mode
- `contexts/review.md` - For review mode
- `README.md` - Overview of contexts
