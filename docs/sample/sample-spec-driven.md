# Sample Walkthrough: Use Case 3 — Spec-Driven Development

> **Don't want to build your own agentic template?** Follow this step-by-step guide to execute the pre-built spec-driven workflow using the example agents and prompts included in this repo.

---

## What You'll Use

| Asset | Location | Purpose |
|---|---|---|
| **Agents** | `.github/agents/` | `@spec-coach` |
| **Prompts** | `.github/prompts/` | `spec-1-brainstorm`, `spec-2-setup` |
| **Skills** | `.github/skills/` | `spec-driven-guide`, `find-skills` |
| **MCP Servers** | `.vscode/mcp.json` | Playwright MCP (E2E testing), Azure MCP (deployment) |

## Agent Workflow

```
@spec-coach → @spec-coach → Spec Kit/OpenSpec commands
(brainstorm)   (setup)       (specify → implement → test → deploy)
```

---

## Prerequisites

Before starting, ensure you have the following installed:

### Node.js 20+ (for OpenSpec and Playwright)

Download from [https://nodejs.org](https://nodejs.org) or install via a package manager:

```bash
# macOS (Homebrew)
brew install node

# Windows (winget)
winget install OpenJS.NodeJS.LTS

# Linux (nvm — recommended)
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
nvm install 20
```

Verify: `node --version` (should show v20+)

### Python 3.12+ with uv (for Spec Kit)

Install Python from [https://www.python.org/downloads/](https://www.python.org/downloads/) or:

```bash
# macOS (Homebrew)
brew install python@3.12

# Windows (winget)
winget install Python.Python.3.12
```

Then install **uv** (fast Python package manager):

```bash
# macOS / Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Verify: `python3 --version` (should show 3.12+) and `uv --version`

> **uv docs**: [https://docs.astral.sh/uv/](https://docs.astral.sh/uv/)

### Playwright (for E2E testing)

The Playwright **MCP server** is already configured in `.vscode/mcp.json` and bundles its own browser — no extra setup needed for that.

To run Playwright **E2E test suites** from the terminal (Step 5), install the test runner and its browsers:

```bash
npm init playwright@latest   # scaffolds config + test folder
npx playwright install --with-deps msedge
```

### Azure CLI (for deployment)

Install from [https://learn.microsoft.com/cli/azure/install-azure-cli](https://learn.microsoft.com/cli/azure/install-azure-cli) or:

```bash
# macOS (Homebrew)
brew install azure-cli

# Windows (winget)
winget install Microsoft.AzureCLI

# Linux (script)
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

Log in using credentials from the hackathon coaches:

- [ ] Azure CLI authenticated:
  ```bash
  az login
  az account show --query "{name:name, id:id, tenantId:tenantId}" -o table
  ```
  > Confirm the displayed subscription and tenant with the coaches before deploying.
- [ ] Azure MCP and Playwright MCP servers connected (verify in Copilot Chat)

---

## Step 1: Brainstorm Your App Idea

**Run prompt**: `spec-1-brainstorm`

This invokes `@spec-coach` to help you define your application:

**What it asks you**:
- What problem does this app solve?
- Who is the target user?
- What are 3-5 core features?
- Any tech stack preferences?
- What data does it manage?

**Example ideas the coach may suggest**:
| App | Description |
|---|---|
| Task Board | Kanban-style task management with drag-and-drop |
| Expense Tracker | Log expenses with categories and monthly summaries |
| Recipe Book | Save, search, and rate cooking recipes |
| Habit Tracker | Track daily habits with streaks and charts |
| Meeting Notes | Capture, tag, and search meeting notes |

**What it produces**:
- App name and one-liner description
- 3-5 user stories in "As a [role], I want [action] so that [benefit]" format
- Acceptance criteria for each user story
- Basic data model (entities and relationships)

**Example output** (TaskFlow app):
```
User Story 1: As a user, I want to see a list of my tasks so I know what to do
  - AC: Tasks displayed in a list with title, priority, and status
  - AC: Empty state shows "No tasks yet" message

User Story 2: As a user, I want to add a new task so I can track things to do
  - AC: Input field with "What needs to be done?" placeholder
  - AC: "Add" button creates the task and clears the input
  - AC: Empty titles are rejected with an error message

Data Model:
  Task { id, title, completed, priority, createdAt }
```

**Verify before continuing**:
- [ ] App idea is defined with a clear purpose
- [ ] 3-5 user stories with acceptance criteria
- [ ] Data model covers all features
- [ ] Scope is realistic for a hackathon (not too ambitious)

### Copy/Paste Commands — Kanban Task Board (Drag-and-Drop)

Use these in **Copilot Chat**:
```
spec-1-brainstorm
We are building a Kanban-style task management app with drag-and-drop between columns.
```

---

## Step 2: Set Up Your Spec-Driven Project

**Run prompt**: `spec-2-setup`

This invokes `@spec-coach` to initialize your project tooling:

**Choose your tool**:

### Option A: Spec Kit (Python)
```bash
specify init --here --ai copilot
```
Commands you'll use later:
- `/speckit.constitution` — Set project constitution
- `/speckit.specify` — Write specifications
- `/speckit.plan` — Generate implementation plan
- `/speckit.tasks` — List implementation tasks
- `/speckit.implement` — Generate code from specs

### Option B: OpenSpec (Node.js)
```bash
npm install -g @fission-ai/openspec@latest
openspec init
```
Commands you'll use later:
- `/opsx:propose <idea>` — Propose a feature
- `/opsx:apply` — Implement the proposal
- `/opsx:archive` — Archive completed changes

> **Important**: Run Spec Kit and OpenSpec init from the **repo root** so their prompts and agents are recognized in this workspace.

**Discover skills** (the `find-skills` skill is already installed):
```bash
npx skills find "task management"  # or your app's domain
```

**Verify before continuing**:
- [ ] Spec-driven project is initialized (config files present)
- [ ] Any relevant skills are installed
- [ ] You can run the spec tool commands without errors

> **From here on**: Use the Spec Kit or OpenSpec commands for specify → implement → test → deploy. Do not create custom prompts or agents unless you need to extend beyond those steps.

---

## Step 3: Write Your Specifications

Use the Spec Kit or OpenSpec commands to write specifications for each core feature:

**Key principle**: Specify WHAT to build, not HOW. Focus on behavior, not implementation details.

**What it guides you through**:
- One spec per user story / feature
- Each spec includes: description, acceptance criteria, data model, user interactions, edge cases
- Specs are independent (can be implemented in any order)

**Run the spec tool**:
```bash
# Spec Kit
/speckit.specify

# OpenSpec
/opsx:propose "Add new task with title, priority, and validation"
```

**Example spec for "Add Task" feature**:
```
Feature: Add New Task

As a user, I want to add a new task so that I can track new things to do.

Acceptance Criteria:
- Main page shows an input field with placeholder "What needs to be done?"
- "Add" button next to the input
- Typing a title and clicking "Add" creates the task in the list
- Input is cleared after adding
- New tasks default to "medium" priority and "not completed"
- Empty titles are rejected with a visible error
- Titles longer than 200 characters are truncated

Data:
- Creates a Task with auto-generated ID and current timestamp
```

**Verify before continuing**:
- [ ] Specs exist for all 3-5 core features
- [ ] Each spec has clear acceptance criteria
- [ ] Specs describe WHAT, not HOW (no implementation details)
- [ ] Edge cases are covered (empty input, max length, etc.)

---

## Step 4: Generate the Implementation

Generate the application from your specifications using your chosen spec tool:

**Spec Kit workflow**:
```bash
/speckit.plan       # Generate implementation plan from specs
/speckit.tasks      # List all implementation tasks
/speckit.implement  # Generate the code
```

**OpenSpec workflow**:
```bash
/opsx:apply         # Apply all proposed features
```

**What it produces**: A working web application with:
- All components matching your specs
- Data model implemented
- UI matching acceptance criteria
- Local development server

**Start and verify locally**:
```bash
npm install
npm run dev
# Open http://localhost:3000
```

**Verify before continuing**:
- [ ] App starts without errors
- [ ] Each user story's acceptance criteria work when tested manually
- [ ] Data model matches what was specified
- [ ] UI is usable (not just functional)

---

## Step 5: Write and Run E2E Tests

Use the Playwright MCP server to write and execute tests:

**What it does**:
1. Initializes Playwright if not already set up: `npm init playwright@latest`
2. Writes test files in `tests/` — one test per user story
3. Each test covers: happy path, validation, edge cases, data persistence
4. Runs all tests and fixes failures

**Example test structure**:
```typescript
// tests/todo.spec.ts
import { test, expect } from '@playwright/test';

test.describe('TaskFlow App', () => {
  test.beforeEach(async ({ page }) => {
    await page.goto('/');
  });

  test('displays empty state message', async ({ page }) => {
    await expect(page.locator('[data-testid="empty-state"]'))
      .toContainText('No tasks yet');
  });

  test('user can add a new task', async ({ page }) => {
    await page.fill('[data-testid="task-input"]', 'Buy groceries');
    await page.click('[data-testid="add-button"]');
    await expect(page.locator('[data-testid="task-list"]'))
      .toContainText('Buy groceries');
  });

  test('rejects empty task title', async ({ page }) => {
    await page.click('[data-testid="add-button"]');
    await expect(page.locator('[data-testid="error-message"]'))
      .toBeVisible();
  });

  test('user can mark task as complete', async ({ page }) => {
    await page.fill('[data-testid="task-input"]', 'Buy groceries');
    await page.click('[data-testid="add-button"]');
    await page.click('[data-testid="task-checkbox"]');
    await expect(page.locator('[data-testid="task-item"]'))
      .toHaveClass(/completed/);
  });

  test('user can delete a task', async ({ page }) => {
    await page.fill('[data-testid="task-input"]', 'Temporary task');
    await page.click('[data-testid="add-button"]');
    await page.click('[data-testid="delete-button"]');
    await expect(page.locator('[data-testid="task-list"]'))
      .not.toContainText('Temporary task');
  });
});
```

**Run tests**:
```bash
npx playwright test              # Run all tests headless
npx playwright test --ui         # Visual test runner
npx playwright show-report       # View HTML report
```

**Verify before continuing**:
- [ ] Test files exist in `tests/` directory
- [ ] All tests pass (`npx playwright test` shows green)
- [ ] Each user story has at least one test
- [ ] Edge cases are tested (empty input, long text)

---

## Step 6: Deploy to Azure

Use the Azure MCP server to deploy your application:

**Deployment options** (the agent will recommend based on your app):

| Option | Best For | Command |
|---|---|---|
| **Static Web Apps** | SPAs (React, Vue, vanilla JS) | `az staticwebapp create` |
| **App Service** | Full-stack apps (Next.js, Express) | `az webapp up` |
| **Container Apps** | Containerized microservices | `az containerapp up` |

**Example deployment (Static Web Apps)**:
```bash
npm run build
az staticwebapp create \
  --name taskflow-app \
  --resource-group rg-taskflow-dev-westeurope \
  --source ./dist \
  --location westeurope
```

**Post-deployment verification**:
- [ ] App is accessible at the Azure URL
- [ ] All features work on the deployed version
- [ ] Run Playwright tests against the deployed URL:
  ```bash
  BASE_URL=https://your-app.azurestaticapps.net npx playwright test
  ```

---

## Feature Expansion

After the MVP is deployed, add new features using the same specify → implement → test cycle:

### Spec Kit
```bash
export SPECIFY_FEATURE="dark-mode"
/speckit.specify    # Write spec for dark mode
/speckit.implement  # Generate the code
# Write Playwright test for dark mode toggle
npx playwright test
# Re-deploy
```

### OpenSpec
```bash
/opsx:propose "Add dark mode with toggle and system preference detection"
/opsx:apply
# Test and deploy
```

---

## Expected Final Output

After completing all steps, your repo should contain:

```
src/                          # Application source code
├── components/               # UI components
├── ...
tests/
├── todo.spec.ts              # Playwright E2E tests
├── ...
specs/                        # Specifications (Spec Kit or OpenSpec)
├── ...
playwright.config.ts          # Playwright configuration
package.json
```

Plus a deployed application on Azure accessible via HTTPS, with all Playwright tests passing.
