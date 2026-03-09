---
name: spec-driven-guide
description: Guide for Spec Kit and OpenSpec spec-driven development. Use when setting up spec-driven workflows, choosing between Spec Kit and OpenSpec, writing specs, running slash commands, or troubleshooting missing commands in Copilot Chat. Covers init in existing repos, core workflows, feature isolation, and references to official docs.
---

# Spec-Driven Development Guide

Short, practical guidance for running Spec Kit or OpenSpec in this repo.

## When to Use This Skill

Use when the user asks about:
- Spec-driven development workflows or principles
- Spec Kit or OpenSpec setup and commands
- Running slash commands like `/speckit.specify` or `/opsx:propose`
- Missing commands in Copilot Chat after init
- Working in an existing repository (no new folder)

## Prerequisites

- Spec Kit: Python 3.11+ and `uv`
- OpenSpec: Node.js 20.19.0+
- Run init from the repo root so prompts and agents are registered

## Choosing Spec Kit vs OpenSpec

| Factor | Spec Kit | OpenSpec |
|---|---|---|
| **Language** | Python (requires `uv`) | Node.js (npm package) |
| **Commands** | 8 specialized commands (constitution, clarify, analyze, checklist) | 3 core commands (propose, apply, archive) |
| **Feature isolation** | Manual env var: `export SPECIFY_FEATURE="name"` | Automatic folder per feature: `openspec/changes/<name>/` |
| **Workflow focus** | Explicit quality steps (clarify, analyze, checklist) | Streamlined propose → apply → archive |
| **Best for** | Teams wanting explicit quality gates and detailed planning phases | Teams preferring minimal commands and folder-based organization |
| **Learning curve** | Steeper (more commands to learn) | Gentler (fewer commands) |
| **Customization** | Constitution-driven principles and quality bar | Profile-driven slash command expansion |

### Quick Decision Guide

**Choose Spec Kit if you:**
- Have a Python environment already setup
- Want detailed quality commands (clarify, analyze, checklist)
- Prefer explicit control over each workflow phase
- Need constitution-driven project principles

**Choose OpenSpec if you:**
- Have a Node.js environment already setup
- Want a streamlined propose → apply → archive flow
- Prefer automatic feature folder organization
- Want simpler command surface (fewer slash commands)

**Either works well if you:**
- Are building greenfield apps with spec-first methodology
- Want to avoid git branches for feature isolation
- Need to integrate with GitHub Copilot Chat slash commands

## Spec Kit (Spec Kit CLI)

### Install
```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
```

### Initialize in the current repo
```bash
specify init --here --ai copilot
```

### Core slash commands
| Command | Purpose |
|---|---|
| `/speckit.constitution` | Define project principles and quality bar |
| `/speckit.specify` | Write specifications (what, not how) |
| `/speckit.plan` | Create an implementation plan |
| `/speckit.tasks` | Break plan into executable tasks |
| `/speckit.implement` | Execute tasks to build the feature |

### Optional quality commands
| Command | Purpose |
|---|---|
| `/speckit.clarify` | Clarify underspecified areas before planning |
| `/speckit.analyze` | Check cross-artifact consistency |
| `/speckit.checklist` | Generate QA and completeness checklists |

### Feature isolation (no git branches)
```bash
export SPECIFY_FEATURE="feature-name"
# All operations now scope to this feature
```

## OpenSpec

### Install
```bash
npm install -g @fission-ai/openspec@latest
```

### Initialize in the current repo
```bash
openspec init
```

### Core slash commands
| Command | Purpose |
|---|---|
| `/opsx:propose <idea>` | Create a proposal and spec artifacts |
| `/opsx:apply` | Implement tasks from the spec artifacts |
| `/opsx:archive` | Archive completed changes |

### Where OpenSpec stores artifacts
`openspec/changes/<feature-name>/` contains proposal, specs, design, and tasks.

### Update OpenSpec guidance (if commands feel stale)
```bash
openspec update
```

## Recommended Workflow

1. Brainstorm the app idea and user stories
2. Initialize Spec Kit or OpenSpec in the repo root
3. Specify features (user stories + acceptance criteria)
4. Plan tasks and implement
5. Test with Playwright
6. Iterate feature-by-feature

## Troubleshooting

| Issue | Fix |
|---|---|
| Slash commands not found | Re-run init in the repo root; restart Copilot Chat |
| OpenSpec commands outdated | Run `openspec update` in the repo |
| Spec Kit not in PATH | Reinstall with `uv tool install ...` and reopen terminal |
| Commands work but feel stale | Restart VS Code to reload prompts and agents |
| Spec Kit feature isolation not working | Verify `export SPECIFY_FEATURE="name"` is set in current shell; feature must be lowercase with hyphens |
| Want to switch from Spec Kit to OpenSpec | Both can coexist; just run `openspec init` and use `/opsx:*` commands; previous `.prompts/` and `.agents/` remain |
| OpenSpec proposals not creating artifacts | Check `openspec/changes/` folder exists; if missing, re-run `openspec init` |
| Commands don't appear in Copilot Chat | Check `.prompts/` and `.agents/` folders exist in repo root; if not, init was run in wrong directory |
| Spec Kit constitution not being followed | Re-run `/speckit.constitution` and ensure it's committed to `memory/constitution.md` |
| Feature-by-feature workflow unclear | See Recommended Workflow section; each feature follows: specify → plan → implement → test → archive cycle |

## References

- Spec Kit: https://github.com/github/spec-kit
- Spec Kit docs: https://github.github.io/spec-kit/
- OpenSpec: https://github.com/Fission-AI/OpenSpec/
- OpenSpec docs: https://github.com/Fission-AI/OpenSpec/blob/main/docs/getting-started.md
