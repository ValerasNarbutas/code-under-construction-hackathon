---
agent: 'spec-coach'
description: 'Set up spec-driven development tooling with Spec Kit or OpenSpec and discover relevant skills'
---

# Step 2: Set Up Spec-Driven Development

Initialize your spec-driven project with your chosen tooling.

## Choose Your Tool

### Option A: Spec Kit
Run from the repo root so Spec Kit registers its prompts and agents in this workspace.
```bash
specify init --here --ai copilot
```

Then use these commands:
- `/speckit.constitution` — Review the project constitution
- `/speckit.specify` — Create specifications
- `/speckit.plan` — Generate implementation plan
- `/speckit.tasks` — Break into tasks
- `/speckit.implement` — Implement from specs

### Option B: OpenSpec
Run from the repo root so OpenSpec registers its prompts and agents in this workspace.
```bash
openspec init
```

Then use these commands:
- `/opsx:propose <your-idea>` — Propose your application idea
- `/opsx:apply` — Apply specification as code
- `/opsx:archive` — Archive completed spec

## Discover Skills

The `find-skills` skill is already installed. Use it to discover relevant skills, then install any you want.

Search for skills relevant to your application domain:

```bash
npx skills find "<your domain>"
```

Examples:
```bash
npx skills find "react dashboard"
npx skills find "express api authentication"
npx skills find "tailwind css components"
```

Install any useful skills that are found.

## Expected Output

1. Initialized spec-driven project (Spec Kit or OpenSpec)
2. Discovered and installed relevant domain skills
3. Ready to write specifications

## Next Step

Proceed to writing specifications using your chosen spec tool commands.
