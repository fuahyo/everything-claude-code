# Strategic Compact Skill

Provides manual compaction suggestions to optimize context window usage.

## Purpose

This skill helps manage context window size by:
- **Identifying compaction opportunities** - Finding sections that can be summarized
- **Suggesting strategic compactions** - Recommending what to compact and when
- **Preserving important context** - Ensuring critical information isn't lost
- **Optimizing token usage** - Reducing context size without losing essential information

## When to Use

Use this skill when:
- Context window is approaching limits
- Session has accumulated significant history
- You want to optimize token usage
- Long-running sessions need optimization

## When NOT to Use

- At the start of sessions (not enough context to compact)
- When context is already small
- When all context is actively needed
- During critical debugging (might lose important details)

## How It Works

### 1. Context Analysis
The skill analyzes current context to identify:
- **Redundant information** - Repeated explanations or code
- **Completed tasks** - Finished work that can be summarized
- **Historical context** - Old information no longer relevant
- **Large code blocks** - Code that can be referenced instead of included

### 2. Compaction Suggestions
The skill suggests:
- **What to compact** - Specific sections or topics
- **How to summarize** - Suggested summary format
- **What to preserve** - Critical information to keep
- **When to compact** - Optimal timing for compaction

### 3. Manual Compaction
You manually apply suggested compactions:
- Review suggestions
- Apply compactions you agree with
- Preserve information you need
- Verify nothing critical is lost

## Usage

### Automatic Suggestions
The skill can be configured to suggest compactions:
- When context exceeds thresholds
- At regular intervals
- Before critical operations

### Manual Invocation
Use the suggestion script:

```bash
./suggest-compact.sh
```

This analyzes context and provides compaction recommendations.

### Hook Integration
The skill can be integrated with hooks to suggest compactions automatically:

```json
{
  "matcher": "context_length > 150000",
  "hooks": [{
    "type": "command",
    "command": "~/.claude/skills/strategic-compact/suggest-compact.sh"
  }]
}
```

## Compaction Strategies

### 1. Summarize Completed Work
Instead of keeping full implementation history:
```markdown
## Completed: Market Search Feature
- Implemented semantic search with Redis vector search
- Added fallback to substring search
- Created API endpoint /api/markets/search
- Tests passing, 85% coverage
```

### 2. Reference Instead of Include
Instead of full code blocks:
```markdown
## Implementation Details
See: src/lib/search.ts (searchMarkets function)
Key points: Uses OpenAI embeddings, Redis KNN search, 600ms debounce
```

### 3. Consolidate Similar Information
Merge related context:
```markdown
## Database Schema (Consolidated)
- markets: id, name, slug, description, status, created_at
- trades: id, user_id, market_id, position, amount, created_at
- users: id, email, wallet_address, created_at
[Full schema in docs/database.md]
```

### 4. Remove Redundant Explanations
Keep only the most recent or comprehensive explanation.

## Best Practices

1. **Preserve active context** - Don't compact information you're currently using
2. **Keep critical details** - Maintain essential information for current task
3. **Summarize, don't delete** - Replace with summaries, not removal
4. **Review suggestions** - Don't auto-apply all suggestions
5. **Test after compaction** - Verify nothing important was lost

## Example Suggestion

```
╔══════════════════════════════════════════════════════════╗
║          Strategic Compaction Suggestion                  ║
╠══════════════════════════════════════════════════════════╣
║ Current Context: 185,432 tokens                          ║
║ Suggested Reduction: ~45,000 tokens                      ║
╚══════════════════════════════════════════════════════════╝

## Recommended Compactions

### 1. Summarize Completed Features (High Impact)
**Current:** Full implementation history of market search feature
**Suggested:** Summary of what was implemented
**Savings:** ~25,000 tokens

### 2. Reference Code Instead of Including (Medium Impact)
**Current:** Full code blocks for utility functions
**Suggested:** File references with key points
**Savings:** ~15,000 tokens

### 3. Consolidate Database Schema (Low Impact)
**Current:** Multiple schema descriptions
**Suggested:** Single consolidated schema
**Savings:** ~5,000 tokens

## What to Preserve
- Current task context
- Recent error messages
- Active debugging information
- Unresolved questions
```

## Notes / Limitations

- **Manual process** - Requires review and approval
- **Risk of information loss** - Must carefully review what to compact
- **Context-dependent** - Suggestions vary by session content
- **Not automatic** - You control what gets compacted

## Related Files

- `suggest-compact.sh` - Compaction suggestion script
- [Hooks](../../hooks/strategic-compact/) - Hook integration examples

---

**See also:**
- [Main README](../../README.md) - Overview of repository
- [Longform Guide](https://x.com/affaanmustafa/status/2014040193557471352) - Advanced context management
- [Memory Persistence](../../hooks/memory-persistence/) - Session state management
