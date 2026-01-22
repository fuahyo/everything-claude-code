---
description: Fixes TypeScript and build errors incrementally with minimal changes. Invokes build-error-resolver agent to get builds passing quickly.
---

# Build Fix Command

This command invokes the **build-error-resolver** agent to fix TypeScript and build errors quickly and efficiently.

## What This Command Does

1. **Runs build** - Executes `npm run build` or `pnpm build`
2. **Parses errors** - Groups errors by file and sorts by severity
3. **Fixes incrementally** - Addresses one error at a time
4. **Verifies fixes** - Re-runs build after each fix
5. **Provides summary** - Shows what was fixed and what remains

## When to Use

Use `/build-fix` when:
- Build is failing with TypeScript errors
- Compilation errors are blocking development
- Import/module resolution issues occur
- Type errors need quick resolution
- You need to get the build green quickly

## When NOT to Use

- For refactoring (use `/refactor-clean`)
- For architectural changes (use `/plan` first)
- When build is passing
- For logic errors (fix manually)
- When you need to understand why errors occurred (investigate first)

## How It Works

The build-error-resolver agent will:

1. **Run build**: `npm run build` or `pnpm build`

2. **Parse error output**:
   - Group by file
   - Sort by severity
   - Identify error types (type errors, import errors, etc.)

3. **For each error**:
   - Show error context (5 lines before/after)
   - Explain the issue clearly
   - Propose minimal fix
   - Apply fix
   - Re-run build
   - Verify error resolved

4. **Stop if**:
   - Fix introduces new errors
   - Same error persists after 3 attempts
   - User requests pause

5. **Show summary**:
   - Errors fixed
   - Errors remaining
   - New errors introduced (if any)

## Example Usage

```
User: /build-fix

Agent (build-error-resolver):
# Build Error Resolution

Running build...
❌ Build failed with 3 errors

## Error 1: Type Inference Failure
**File:** `src/components/MarketCard.tsx:45`
**Error:** Parameter 'market' implicitly has an 'any' type

**Context:**
```typescript
function formatMarket(market) {  // Line 45
  return market.name
}
```

**Fix:** Add type annotation
```typescript
function formatMarket(market: Market) {
  return market.name
}
```

Applying fix...
✅ Error resolved

## Error 2: Missing Import
**File:** `src/lib/utils.ts:12`
**Error:** Cannot find module '@/types'

**Fix:** Add missing import or fix path
...

## Summary
- Errors fixed: 3
- Errors remaining: 0
- Build status: ✅ PASSING
```

## Integration

This command invokes the `build-error-resolver` agent located at:
`~/.claude/agents/build-error-resolver.md`

The agent uses tools: Read, Write, Edit, Bash, Grep, Glob

## Related Commands

- `/code-review` - Review code after build passes
- `/tdd` - Write tests (may reveal type issues)
- `/plan` - Plan changes if errors indicate architectural issues

## Important Notes

**CRITICAL**: Fix one error at a time for safety!

The agent focuses on:
- **Minimal changes** - Only fixes what's necessary
- **No refactoring** - Doesn't change architecture or logic
- **Quick resolution** - Gets build green as fast as possible
- **Verification** - Re-runs build after each fix

If errors persist after 3 attempts, the agent will stop and ask for guidance.
