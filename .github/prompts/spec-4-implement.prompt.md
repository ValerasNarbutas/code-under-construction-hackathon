---
agent: 'spec-coach'
description: 'Generate the application implementation from specifications'
---

# Step 4: Implement from Specifications

Let AI generate the application code from your specifications.

## Implementation

### Using Spec Kit
```
/speckit.plan       # Generate implementation plan from specs
/speckit.tasks      # Break plan into actionable tasks
/speckit.implement  # Implement from specifications
```

### Using OpenSpec
```
/opsx:apply         # Apply the specification as code
```

## Implementation Review Checklist

After AI generates the code, verify:

- [ ] **Matches specs** — Does the implementation match your specifications?
- [ ] **Runs locally** — Can you start the app with `npm start` or equivalent?
- [ ] **Core features work** — Do the main user stories function correctly?
- [ ] **Data model correct** — Are entities and fields as specified?
- [ ] **UI is usable** — Is the interface functional and navigable?

## Local Development

Start the application locally:
```bash
# Typical commands (depends on your stack)
npm install
npm run dev
```

Verify in browser at `http://localhost:3000` (or the appropriate port).

## Expected Output

A working application that matches your specifications, running locally.

## Next Step

Proceed to `spec-5-test` to write and run Playwright E2E tests.
