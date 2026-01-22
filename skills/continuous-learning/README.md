# Continuous Learning Skill

Automatically extracts patterns from Claude Code sessions into reusable skills.

## Purpose

This skill analyzes completed sessions to identify:
- Error resolution patterns
- User corrections that reveal preferences
- Workarounds for common issues
- Debugging techniques
- Project-specific patterns

These patterns are then extracted into reusable skills that can be invoked in future sessions.

## When to Use

This skill is typically:
- **Automatically invoked** - After sessions meet minimum length threshold
- **Manually triggered** - Via `/learn` command
- **Scheduled** - Run periodically to extract accumulated knowledge

## When NOT to Use

- For one-time fixes that won't recur
- For simple typos or trivial corrections
- For external API issues that are outside your control
- During active development (wait until session completes)

## How It Works

### 1. Session Analysis
The skill analyzes completed sessions for:
- **Error resolution patterns** - How errors were fixed
- **User corrections** - What the user changed and why
- **Workarounds** - Solutions to common problems
- **Debugging techniques** - Effective debugging approaches
- **Project-specific patterns** - Domain knowledge unique to your project

### 2. Pattern Detection
Patterns are detected based on:
- **Frequency** - Patterns that appear multiple times
- **Complexity** - Non-trivial solutions worth preserving
- **Reusability** - Patterns applicable to future sessions
- **Project relevance** - Patterns specific to your codebase

### 3. Skill Generation
Detected patterns are extracted into:
- **Skill files** - Reusable knowledge in `~/.claude/skills/learned/`
- **Documentation** - Explanations of when and how to use patterns
- **Examples** - Code examples demonstrating the pattern

## Configuration

Edit `config.json` to customize behavior:

```json
{
  "min_session_length": 10,
  "extraction_threshold": "medium",
  "auto_approve": false,
  "learned_skills_path": "~/.claude/skills/learned/",
  "patterns_to_detect": [
    "error_resolution",
    "user_corrections",
    "workarounds",
    "debugging_techniques",
    "project_specific"
  ],
  "ignore_patterns": [
    "simple_typos",
    "one_time_fixes",
    "external_api_issues"
  ]
}
```

### Configuration Options

- **min_session_length**: Minimum number of tool calls before analysis
- **extraction_threshold**: "low", "medium", or "high" - how selective to be
- **auto_approve**: Whether to create skills automatically or request approval
- **learned_skills_path**: Where to save extracted skills
- **patterns_to_detect**: Types of patterns to look for
- **ignore_patterns**: Patterns to skip

## Usage

### Automatic Extraction
The skill runs automatically after sessions that:
- Meet minimum length requirement
- Contain extractable patterns
- Complete successfully

### Manual Extraction
Use the `/learn` command to manually extract patterns:

```
/learn
```

This will:
1. Analyze recent sessions
2. Identify extractable patterns
3. Present patterns for review
4. Generate skill files upon approval

### Evaluation Script
The `evaluate-session.sh` script analyzes a session file:

```bash
./evaluate-session.sh session-log.tmp
```

## Example Output

After analysis, you might see:

```markdown
# Extracted Pattern: Supabase RLS Policy Creation

## Pattern Detected
User repeatedly creates Row Level Security policies with similar structure.

## When to Use
- Creating new Supabase tables
- Adding RLS policies
- Securing database access

## Pattern
```sql
ALTER TABLE [table_name] ENABLE ROW LEVEL SECURITY;

CREATE POLICY "[policy_name]"
  ON [table_name] FOR [operation]
  USING (auth.uid() = user_id);
```

## Examples from Sessions
- Session 2026-01-15: Created RLS for markets table
- Session 2026-01-18: Applied same pattern to trades table
```

## Best Practices

1. **Review extracted patterns** - Not all patterns are worth preserving
2. **Refine skills** - Edit generated skills to improve clarity
3. **Test skills** - Verify extracted skills work in practice
4. **Organize learned skills** - Group related skills together
5. **Update regularly** - Run extraction periodically to capture new patterns

## Notes / Limitations

- **Pattern detection is heuristic** - May miss some patterns or flag false positives
- **Requires sufficient session data** - Needs multiple examples to detect patterns
- **Project-specific** - Extracted skills are tailored to your codebase
- **Manual review recommended** - Auto-approve should be used cautiously

## Related Files

- `config.json` - Configuration settings
- `evaluate-session.sh` - Session evaluation script
- `~/.claude/skills/learned/` - Directory for extracted skills

---

**See also:**
- [Main README](../../README.md) - Overview of repository
- [Commands](../../commands/learn.md) - `/learn` command documentation
- [Longform Guide](https://x.com/affaanmustafa/status/2014040193557471352) - Advanced techniques
