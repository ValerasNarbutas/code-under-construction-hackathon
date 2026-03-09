# Spec-Driven Development Guide

> A skill for GitHub Copilot providing quick-reference guidance on spec-driven development methodology.

## Spec Kit Quick Reference

### Installation
```bash
uv tool install specify-cli --from git+https://github.com/github/spec-kit.git
```

### Initialize
```bash
specify init <name> --ai copilot --no-git
```

### Commands
| Command | Purpose |
|---|---|
| `/speckit.constitution` | Review project constitution |
| `/speckit.specify` | Create or refine specifications |
| `/speckit.plan` | Generate implementation plan |
| `/speckit.tasks` | Break plan into tasks |
| `/speckit.implement` | Implement from specs |
| `/speckit.clarify` | Clarify ambiguous specs |
| `/speckit.analyze` | Analyze current state |
| `/speckit.checklist` | Review progress checklist |

### Feature Isolation (no git branches)
```bash
export SPECIFY_FEATURE="feature-name"
# All operations now scope to this feature
```

---

## OpenSpec Quick Reference

### Installation
```bash
npm install -g @fission-ai/openspec@latest
```

### Initialize
```bash
openspec init
```

### Commands
| Command | Purpose |
|---|---|
| `/opsx:propose <idea>` | Propose a feature or app idea |
| `/opsx:apply` | Apply specification as code |
| `/opsx:archive` | Archive completed spec |

### Feature Isolation
Features automatically organized under `openspec/changes/<feature-name>/`

---

## Methodology

1. **Specify WHAT, not HOW** — Describe behavior, not implementation
2. **Start small** — 3-5 core features for MVP
3. **Write user stories** — "As a [role], I want [action] so that [benefit]"
4. **Include acceptance criteria** — How do we know it works?
5. **Test each feature** — Playwright E2E tests validate specs
6. **Iterate** — Add features one at a time, specify → implement → test
