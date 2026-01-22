---
description: Safely identifies and removes dead code with test verification. Invokes refactor-cleaner agent to clean up unused code, duplicates, and dependencies.
---

# Refactor Clean Command

This command invokes the **refactor-cleaner** agent to safely identify and remove dead code, duplicates, and unused dependencies.

## What This Command Does

1. **Runs analysis tools** - Uses knip, depcheck, ts-prune to find unused code
2. **Categorizes findings** - Groups by risk level (SAFE, CAUTION, DANGER)
3. **Proposes safe deletions** - Only suggests verifiably unused code
4. **Verifies with tests** - Runs test suite before and after each deletion
5. **Documents changes** - Creates deletion log for tracking

## When to Use

Use `/refactor-clean` when:
- Codebase has accumulated unused code
- You want to reduce bundle size
- Removing duplicate code
- Cleaning up unused dependencies
- Preparing for codebase maintenance

## When NOT to Use

- During active feature development
- Right before production deployment
- When codebase is unstable
- Without proper test coverage
- When you're unsure about code usage

## How It Works

The refactor-cleaner agent will:

1. **Run dead code analysis tools**:
   - **knip**: Find unused exports and files
   - **depcheck**: Find unused dependencies
   - **ts-prune**: Find unused TypeScript exports
   - **eslint**: Check for unused disable-directives

2. **Generate comprehensive report** in `.reports/dead-code-analysis.md`

3. **Categorize findings by severity**:
   - **SAFE**: Test files, unused utilities, clearly unused exports
   - **CAUTION**: API routes, components, potentially used via dynamic imports
   - **DANGER**: Config files, main entry points, public API

4. **Propose safe deletions only** - Starts with SAFE items

5. **Before each deletion**:
   - Run full test suite
   - Verify tests pass
   - Apply change
   - Re-run tests
   - Rollback if tests fail
   - Update deletion log

6. **Show summary** of cleaned items

## Example Usage

```
User: /refactor-clean

Agent (refactor-cleaner):
# Dead Code Cleanup

Running analysis tools...
✅ knip: Found 15 unused exports
✅ depcheck: Found 3 unused dependencies
✅ ts-prune: Found 8 unused TypeScript exports

## Analysis Report

### SAFE to Remove
- `src/utils/old-helpers.ts` - No references found
- `src/components/OldButton.tsx` - Replaced by Button.tsx
- `package.json`: `lodash` - Not imported anywhere

### CAUTION (Verify First)
- `src/api/legacy-endpoint.ts` - May be used via dynamic import
- `src/components/LegacyModal.tsx` - Check for string-based references

### DANGER (Do Not Remove)
- `src/config.ts` - Main entry point
- `package.json`: `react` - Core dependency

## Proposed Deletions (SAFE items only)

1. Remove unused utility: `src/utils/old-helpers.ts`
   - Running tests...
   ✅ All tests pass
   - Applying deletion...
   ✅ Deleted successfully

2. Remove unused dependency: `lodash`
   - Running tests...
   ✅ All tests pass
   - Removing from package.json...
   ✅ Removed successfully

## Summary
- Files deleted: 5
- Dependencies removed: 3
- Lines of code removed: 1,200
- Bundle size reduction: ~45 KB
- All tests passing: ✅
```

## Integration

This command invokes the `refactor-cleaner` agent located at:
`~/.claude/agents/refactor-cleaner.md`

The agent uses tools: Read, Write, Edit, Bash, Grep, Glob

## Related Commands

- `/code-review` - Review code after cleanup
- `/test-coverage` - Ensure tests cover remaining code
- `/update-docs` - Update documentation after cleanup

## Important Notes

**CRITICAL**: Never delete code without running tests first!

The agent:
- **Starts with SAFE items** - Only removes verifiably unused code
- **Tests before deletion** - Ensures nothing breaks
- **Documents everything** - Creates deletion log
- **Rolls back on failure** - Reverts if tests fail

If you're unsure about a deletion, the agent will ask for confirmation.
