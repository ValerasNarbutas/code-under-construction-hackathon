# Use Case 3: Spec-Driven Development — Greenfield Application

Build a greenfield web application using specification-first methodology with AI-powered implementation.

## Objective

Design, build, and execute your own **spec-driven agentic workflow** — a set of custom agents, prompts, skills, and MCP server configurations — to brainstorm, specify, implement, test, and deploy a web application. Your team decides WHAT to build, chooses the spec-driven tooling, and defines HOW the AI agents orchestrate the process.

## Prerequisites

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

Install Python from [https://www.python.org/downloads/](https://www.python.org/downloads/) or via a package manager:

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

### VS Code with GitHub Copilot

- Download VS Code: [https://code.visualstudio.com](https://code.visualstudio.com)
- Install the **GitHub Copilot** extension from the [VS Code Marketplace](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot)
- Or use **GitHub Codespaces** (no local install needed)

### Playwright (for E2E testing)

The Playwright **MCP server** is already configured in `.vscode/mcp.json` and bundles its own browser — no extra setup needed for that.

However, to run Playwright **E2E test suites** from the terminal (Step 5 of the workflow), you need to install the test runner and its browsers separately:

```bash
npm init playwright@latest   # scaffolds config + test folder
npx playwright install --with-deps msedge
```

### Azure CLI (Required for Deployment)

Install the Azure CLI from [https://learn.microsoft.com/cli/azure/install-azure-cli](https://learn.microsoft.com/cli/azure/install-azure-cli) or:

```bash
# macOS (Homebrew)
brew install azure-cli

# Windows (winget)
winget install Microsoft.AzureCLI

# Linux (script)
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
```

If you plan to deploy your app to Azure, log in first using the credentials provided by the hackathon coaches:

```bash
az login
```

Verify you are on the correct subscription:

```bash
az account show --query "{name:name, id:id, tenantId:tenantId}" -o table
```

> **Important**: Confirm the displayed subscription and tenant with the hackathon coaches before deploying.

---

## Participant Guide

### Phase 1: Define What You Want to Build

Answer these questions as a team:

- [ ] **What application are you building?** (e.g., a task tracker, a recipe app, a dashboard)
- [ ] **Who are the users?** Define 3-5 user stories with acceptance criteria
- [ ] **What features are in scope for the MVP?** Keep it focused (3-5 core features)
- [ ] **What tech stack will you use?** (any web framework — React, Next.js, Vue, plain HTML/JS, etc.)
- [ ] **What data model do you need?** (entities, relationships, persistence)

### Phase 2: Define What You Need (Tools & MCP Servers)

Think about which tools and spec-driven methodology you'll use:

- [ ] **Which spec-driven tool will you use?**
  - **Spec Kit** (Python-based): `specify init --here --ai copilot`
    - Commands: `/speckit.constitution`, `/speckit.specify`, `/speckit.plan`, `/speckit.tasks`, `/speckit.implement`
  - **OpenSpec** (Node.js-based): `openspec init`
    - Commands: `/opsx:propose <idea>`, `/opsx:apply`, `/opsx:archive`
- [ ] **Which MCP servers do you need?**
  - Playwright MCP — for running E2E tests against your app
  - Azure MCP — for deploying to Azure (App Service, Static Web Apps, etc.)
- [ ] **Which skills do you need?**
  - The `find-skills` skill is already installed — use it to discover and install skills
  - Run `npx skills find <domain>` to discover
  - Install any you need with `npx skills add <owner/repo@skill>`
- [ ] **Configure your MCP servers** in `.vscode/mcp.json`

> **Important**: Run both Spec Kit and OpenSpec init from the **repo root**. They install prompts and agents that must be registered at the workspace root to be recognized.

### Phase 3: Execute the Spec-Driven Workflow (No Custom Agents/Prompts Yet)

After `spec-2-setup`, use the Spec Kit or OpenSpec commands for specify → implement → test → deploy.
Do **not** create custom prompts or custom agents unless you truly need to extend the workflow beyond those steps.

Run the workflow in order and verify each step:

1. **Brainstorm** — Run the brainstorm prompt. Verify user stories and acceptance criteria are defined
2. **Setup** — Initialize your spec-driven tool and discover relevant skills
3. **Specify** — Run your spec tool commands. Verify specs cover all core features
4. **Implement** — Run your spec tool commands. Verify the app runs locally
5. **Test** — Write and run Playwright E2E tests. Verify each user story
6. **Deploy** — Deploy using Azure MCP. Verify the app is live

### Phase 4: Verify & Iterate

Review the quality of your outputs:

- [ ] Does the app match the user stories and acceptance criteria?
- [ ] Do all Playwright E2E tests pass?
- [ ] Is the app running locally at `http://localhost:3000` (or similar)?
- [ ] Is the app deployed and accessible on Azure?
- [ ] Can you add a new feature by running the specify → implement → test cycle again?

---

## Feature Expansion

Add new features without git branches — use folder-based feature isolation:

### Spec Kit
```bash
export SPECIFY_FEATURE="new-feature-name"
/speckit.specify    # Specs scoped to this feature
/speckit.implement  # Implementation scoped to this feature
```

### OpenSpec
```
/opsx:propose "Description of the new feature"
/opsx:apply
```

Each feature follows the same cycle: **specify → implement → test → deploy**

---

## Copy/Paste Commands — Kanban Task Board (Drag-and-Drop)

Use these ready-to-paste sequences in **Copilot Chat**. Run terminal commands from the **repo root**.

### Spec Kit

**Copilot Chat**:
```
spec-1-brainstorm
We are building a Kanban-style task management app with drag-and-drop between columns.
```

**Terminal (repo root)**:
```bash
specify init --here --ai copilot
npx skills find "kanban drag and drop"
```

**Copilot Chat**:
```
Use Spec Kit. Create specs for a Kanban board with Backlog, In Progress, and Done columns.
Include drag-and-drop, task creation, editing, and persistence.
Then run /speckit.specify, /speckit.plan, /speckit.tasks, and /speckit.implement.
```

### OpenSpec

**Copilot Chat**:
```
spec-1-brainstorm
We are building a Kanban-style task management app with drag-and-drop between columns.
```

**Terminal (repo root)**:
```bash
openspec init
npx skills find "kanban drag and drop"
```

**Copilot Chat**:
```
Use OpenSpec. Propose and apply specs for a Kanban board with Backlog, In Progress, and Done columns.
Include drag-and-drop, task creation, editing, and persistence.
Then run /opsx:propose and /opsx:apply.
```

---

## Expected File Structure

```
.github/
├── agents/                 # 👈 Your custom agents
│   ├── <your-agent>.agent.md
│   └── ...
├── instructions/           # 🤖 Auto-activating Copilot guidelines (pre-configured)
│   ├── agents.instructions.md
│   ├── prompt.instructions.md
│   ├── agent-skills.instructions.md
│   └── instructions.instructions.md
├── prompts/                # 👈 Your reusable prompts
│   ├── <your-prompt>.prompt.md
│   └── ...
├── skills/                 # 👈 Your custom skills (if any)
│   └── ...
└── copilot-instructions.md # 👈 Workspace-wide context
.vscode/
└── mcp.json                # 👈 Your MCP server configuration
src/                        # 👈 Your application source code
tests/                      # 👈 Playwright E2E tests
specs/                      # 👈 Specifications (Spec Kit or OpenSpec)
```

---

## Stuck? Check the Examples

This repo includes a **complete reference implementation** showing one way to solve this use case:

| What | Where | Purpose |
|---|---|---|
| Example agents | `.github/agents/spec-coach.agent.md` | See how a spec-driven agent is defined |
| Example prompts | `.github/prompts/spec-1-brainstorm.prompt.md`, `spec-2-setup.prompt.md` | See the spec-driven prompts used in this guide |
| Example skills | `.github/skills/spec-driven-guide/` | See how a spec methodology skill is documented |
| Instruction files | `.github/instructions/` | Auto-loaded guidelines for writing agents, prompts, skills, and instructions |
| Example MCP config | `.vscode/mcp.json` | See how Playwright and Azure MCP servers are configured |
| Sample walkthrough | [docs/sample/spec-driven-example.md](sample/spec-driven-example.md) | See what a completed spec-driven workflow looks like |

> **These are just examples** — your team should build your own agents, prompts, and workflow. Use the examples for inspiration when you get stuck.

---

## Tips

- **Start small** — Focus on 3-5 core features for the MVP
- **Specs over code** — Spend more time writing good specs than fixing generated code
- **Test everything** — Write Playwright tests before adding new features
- **Local first** — Get it working locally before deploying to Azure
- **Iterate** — It's better to have 3 polished features than 10 broken ones
- **Build agents incrementally** — Create one agent, test it, then build the next
