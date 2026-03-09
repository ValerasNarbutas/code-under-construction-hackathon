---
agent: 'spec-coach'
description: 'Write application specifications that describe WHAT to build, not HOW'
---

# Step 3: Write Specifications

Create clear, testable specifications for your application features.

## Spec-Driven Principle

**Specify WHAT, not HOW.** Describe the desired behavior and outcomes. Let AI decide the implementation details.

## Writing Specifications

### Using Spec Kit
```
/speckit.specify
```
The tool will guide you through creating specifications interactively.

### Using OpenSpec
```
/opsx:propose <detailed description of your feature>
```

## Specification Quality Checklist

For each feature specification, ensure:

- [ ] **Clear behavior** — What does the user see and do?
- [ ] **Acceptance criteria** — How do we verify it works?
- [ ] **Data model** — What entities and fields are involved?
- [ ] **User interactions** — Click, type, drag, navigate?
- [ ] **Edge cases** — Empty states, errors, limits?
- [ ] **Independent** — Can be built and tested separately?

## Example Specification

```
Feature: Add Todo Item

As a user, I want to add a new todo item so that I can track my tasks.

Acceptance Criteria:
- User sees an input field and an "Add" button on the main page
- User types a task description and clicks "Add"
- The new task appears in the list below the input
- The input field is cleared after adding
- Empty descriptions are rejected with an error message
- Tasks are persisted across page refreshes

Data:
- Todo: { id, title, completed, createdAt }
```

## Expected Output

Complete specifications for your 3-5 core features, ready for implementation.

## Next Step

Proceed to `spec-4-implement` to generate the application from your specifications.
