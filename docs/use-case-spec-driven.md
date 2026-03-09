# Use Case 3: Spec-Driven Development — Greenfield Application

Build a greenfield web application using specification-first methodology with AI-powered implementation.

## Objective

Design, build, and execute your own **spec-driven agentic workflow** — a set of custom agents, prompts, skills, and MCP server configurations — to brainstorm, specify, implement, test, and deploy a web application. Your team decides WHAT to build, chooses the spec-driven tooling, and defines HOW the AI agents orchestrate the process.

## Prerequisites

- Node.js 20+ (for OpenSpec and Playwright)
- Python 3.12+ with uv (for Spec Kit)
- VS Code with GitHub Copilot (or Codespaces)

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
  - **Spec Kit** (Python-based): `specify init <name> --ai copilot --no-git`
    - Commands: `/speckit.constitution`, `/speckit.specify`, `/speckit.plan`, `/speckit.tasks`, `/speckit.implement`
  - **OpenSpec** (Node.js-based): `openspec init`
    - Commands: `/opsx:propose <idea>`, `/opsx:apply`, `/opsx:archive`
- [ ] **Which MCP servers do you need?**
  - Playwright MCP — for running E2E tests against your app
  - Azure MCP — for deploying to Azure (App Service, Static Web Apps, etc.)
- [ ] **Which skills do you need?**
  - Are there domain-specific skills? Run `npx skills find <domain>` to discover
  - Do you need a custom skill for your spec methodology?
- [ ] **Configure your MCP servers** in `.vscode/mcp.json`

### Phase 3: Design Your Agentic Workflow

Plan the agents that will guide your spec-driven process:

- [ ] **What steps does your workflow need?** (e.g., brainstorm → setup → specify → implement → test → deploy)
- [ ] **What agent handles each step?** Define a custom agent (`.github/agents/<name>.agent.md`) for each role
- [ ] **What tools does each agent need?** (Playwright MCP for testing, Azure MCP for deployment)
- [ ] **How do agents hand off to each other?** (e.g., specs feed into implementation, implementation feeds into testing)
- [ ] **What does each agent output?** (e.g., user stories, specifications, working code, test results)

For each agent, create a `.agent.md` file in `.github/agents/` with:
- A clear role description
- The tools it needs access to
- Handoffs to the next agent in the workflow
- Detailed instructions on what it should produce

> **Built-in help**: When you create or edit a `.agent.md` file, Copilot automatically loads the [agents instruction file](../.github/instructions/agents.instructions.md) with guidelines on frontmatter, tools, handoffs, and best practices.

### Phase 4: Write Your Prompts

For each step in your workflow, create a reusable prompt (`.github/prompts/<name>.prompt.md`):

- [ ] **What should each prompt ask the agent to do?** Be specific about the app idea, features, and expected output
- [ ] **What context does each prompt need?** (spec files, user stories, previous output)
- [ ] **Number your prompts sequentially** so they're easy to run in order

> **Built-in help**: When you create or edit a `.prompt.md` file, Copilot automatically loads the [prompt instruction file](../.github/instructions/prompt.instructions.md) with guidelines on frontmatter, structure, inputs, and output definitions.

### Phase 5: Execute Your Workflow

Run your prompts in order and verify each step:

1. **Brainstorm** — Run your brainstorm prompt. Verify user stories and acceptance criteria are defined
2. **Setup** — Initialize your spec-driven tool and discover relevant skills
3. **Specify** — Run your specification prompt. Verify specs cover all core features
4. **Implement** — Run your implementation prompt. Verify the app runs locally
5. **Test** — Run your testing prompt. Verify Playwright E2E tests pass for each user story
6. **Deploy** — Run your deploy prompt. Verify the app is live on Azure

### Phase 6: Verify & Iterate

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
| Example agents | `.github/agents/spec-coach.agent.md`, `qa-engineer.agent.md`, `deployer.agent.md` | See how spec-driven agents are defined |
| Example prompts | `.github/prompts/spec-1-brainstorm.prompt.md`, etc. | See how spec-driven prompts are structured |
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
