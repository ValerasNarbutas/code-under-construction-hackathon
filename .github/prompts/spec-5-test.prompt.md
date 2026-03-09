---
agent: 'qa-engineer'
description: 'Write and run Playwright E2E tests to validate implemented features against specifications'
---

# Step 5: Test with Playwright

Write and run E2E tests to validate every user story.

## Test Setup

Initialize Playwright if not already done:
```bash
npm init playwright@latest
```

## Writing Tests

For each user story, write at least one Playwright test:

```typescript
import { test, expect } from '@playwright/test';

test.describe('Feature: <Feature Name>', () => {
  test.beforeEach(async ({ page }) => {
    await page.goto('/');
  });

  test('<user story description>', async ({ page }) => {
    // Arrange: set up preconditions
    // Act: perform the user action
    // Assert: verify the expected outcome
  });
});
```

## Test Coverage Goals

For each user story:
- [ ] **Happy path** — The primary flow works
- [ ] **Validation** — Invalid inputs are handled
- [ ] **Edge cases** — Empty states, boundaries
- [ ] **Persistence** — Data survives page refresh (if specified)

## Running Tests

```bash
# Run all tests
npx playwright test

# Run with UI mode (visual debugging)
npx playwright test --ui

# Run specific test file
npx playwright test tests/todo.spec.ts
```

Or use the Playwright MCP server to run tests interactively through Copilot.

## Expected Output

1. Playwright test files in `tests/` directory
2. All tests passing for core user stories
3. Test report showing pass/fail status

## Next Step

Proceed to `spec-6-deploy` to deploy your application to Azure.
