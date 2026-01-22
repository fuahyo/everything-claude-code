# TDD Workflow Skill

Enforces test-driven development methodology with comprehensive test coverage requirements.

## Purpose

This skill ensures all code development follows TDD principles:
- **Tests before code** - Write failing tests first
- **Comprehensive coverage** - 80%+ coverage requirement
- **Multiple test types** - Unit, integration, and E2E tests
- **Quality assurance** - Catch bugs before production

## When to Use

This skill activates automatically when:
- Writing new features or functionality
- Fixing bugs or issues
- Refactoring existing code
- Adding API endpoints
- Creating new components

## When NOT to Use

- Documentation-only changes
- Configuration updates
- Simple formatting changes
- Non-code changes

## Core Principles

### 1. Tests BEFORE Code
ALWAYS write tests first, then implement code to make tests pass.

### 2. Coverage Requirements
- Minimum 80% coverage (unit + integration + E2E)
- All edge cases covered
- Error scenarios tested
- Boundary conditions verified

### 3. Test Types

#### Unit Tests
- Individual functions and utilities
- Component logic
- Pure functions
- Helpers and utilities

#### Integration Tests
- API endpoints
- Database operations
- Service interactions
- External API calls

#### E2E Tests (Playwright)
- Critical user flows
- Complete workflows
- Browser automation
- UI interactions

## TDD Workflow Steps

### Step 1: Write User Journeys
```
As a [role], I want to [action], so that [benefit]
```

### Step 2: Generate Test Cases
Create comprehensive test cases for each user journey.

### Step 3: Run Tests (They Should Fail)
Verify tests fail before implementation.

### Step 4: Implement Code
Write minimal code to make tests pass.

### Step 5: Run Tests Again
Verify tests now pass.

### Step 6: Refactor
Improve code quality while keeping tests green.

### Step 7: Verify Coverage
Ensure 80%+ coverage achieved.

## Test Patterns

### Unit Test Pattern
```typescript
import { render, screen, fireEvent } from '@testing-library/react'
import { Button } from './Button'

describe('Button Component', () => {
  it('renders with correct text', () => {
    render(<Button>Click me</Button>)
    expect(screen.getByText('Click me')).toBeInTheDocument()
  })
})
```

### API Integration Test Pattern
```typescript
import { NextRequest } from 'next/server'
import { GET } from './route'

describe('GET /api/markets', () => {
  it('returns markets successfully', async () => {
    const request = new NextRequest('http://localhost/api/markets')
    const response = await GET(request)
    const data = await response.json()

    expect(response.status).toBe(200)
    expect(data.success).toBe(true)
  })
})
```

### E2E Test Pattern (Playwright)
```typescript
import { test, expect } from '@playwright/test'

test('user can search and filter markets', async ({ page }) => {
  await page.goto('/markets')
  await page.fill('input[placeholder="Search markets"]', 'election')
  await page.waitForTimeout(600)
  
  const results = page.locator('[data-testid="market-card"]')
  await expect(results).toHaveCount(5, { timeout: 5000 })
})
```

## Test File Organization

```
src/
├── components/
│   ├── Button/
│   │   ├── Button.tsx
│   │   ├── Button.test.tsx          # Unit tests
│   │   └── Button.stories.tsx
│   └── MarketCard/
│       ├── MarketCard.tsx
│       └── MarketCard.test.tsx
├── app/
│   └── api/
│       └── markets/
│           ├── route.ts
│           └── route.test.ts         # Integration tests
└── e2e/
    ├── markets.spec.ts               # E2E tests
    └── trading.spec.ts
```

## Mocking External Services

### Supabase Mock
```typescript
jest.mock('@/lib/supabase', () => ({
  supabase: {
    from: jest.fn(() => ({
      select: jest.fn(() => ({
        eq: jest.fn(() => Promise.resolve({
          data: [{ id: 1, name: 'Test Market' }],
          error: null
        }))
      }))
    }))
  }
}))
```

### Redis Mock
```typescript
jest.mock('@/lib/redis', () => ({
  searchMarketsByVector: jest.fn(() => Promise.resolve([
    { slug: 'test-market', similarity_score: 0.95 }
  ]))
}))
```

## Coverage Verification

### Run Coverage Report
```bash
npm run test:coverage
```

### Coverage Thresholds
```json
{
  "jest": {
    "coverageThresholds": {
      "global": {
        "branches": 80,
        "functions": 80,
        "lines": 80,
        "statements": 80
      }
    }
  }
}
```

## Common Mistakes to Avoid

### ❌ WRONG: Testing Implementation Details
```typescript
expect(component.state.count).toBe(5)
```

### ✅ CORRECT: Test User-Visible Behavior
```typescript
expect(screen.getByText('Count: 5')).toBeInTheDocument()
```

### ❌ WRONG: Brittle Selectors
```typescript
await page.click('.css-class-xyz')
```

### ✅ CORRECT: Semantic Selectors
```typescript
await page.click('[data-testid="submit-button"]')
```

## Best Practices

1. **Write Tests First** - Always TDD
2. **One Assert Per Test** - Focus on single behavior
3. **Descriptive Test Names** - Explain what's tested
4. **Arrange-Act-Assert** - Clear test structure
5. **Mock External Dependencies** - Isolate unit tests
6. **Test Edge Cases** - Null, undefined, empty, large
7. **Test Error Paths** - Not just happy paths
8. **Keep Tests Fast** - Unit tests < 50ms each
9. **Clean Up After Tests** - No side effects
10. **Review Coverage Reports** - Identify gaps

## Success Metrics

- 80%+ code coverage achieved
- All tests passing (green)
- No skipped or disabled tests
- Fast test execution (< 30s for unit tests)
- E2E tests cover critical user flows
- Tests catch bugs before production

## Related Files

- `SKILL.md` - Full skill documentation with detailed examples
- [TDD Command](../../commands/tdd.md) - Command that uses this skill
- [TDD Guide Agent](../../agents/tdd-guide.md) - Agent that enforces TDD

---

**See also:**
- [Main README](../../README.md) - Overview of repository
- [Commands](../../commands/tdd.md) - `/tdd` command documentation
- [Agents](../../agents/tdd-guide.md) - TDD guide agent
