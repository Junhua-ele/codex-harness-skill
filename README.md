# Harness Engineering Skill

This Codex skill turns a PRD, rough product idea, or existing project plan into an agent-ready engineering knowledge base.

It is intended for projects that need structured product, design, frontend, technical, architecture, feature, and agent handoff documentation before implementation begins.

## When To Use

Use this skill when a project needs any of the following:

- A complete documentation foundation from a product idea or PRD.
- Agent-ready handoff files for Codex or another coding agent.
- Structured feature specifications with acceptance criteria.
- A machine-readable feature checklist.
- Clear links between product intent, design rules, frontend architecture, technical constraints, and implementation guidance.

Typical trigger requests include:

- "Create engineering docs from this PRD."
- "Turn this product idea into agent-ready specs."
- "Generate PRD, design, architecture, and feature specs."
- "Build a Harness Engineering knowledge base."
- "Update the project docs into the Harness format."

## What It Creates

The skill creates or updates this project-root structure:

```text
PRD.md
DESIGN.md
FRONTEND.md
TECH-SPEC.md
ARCHITECTURE.md
AGENTS.md
README.md
feature-list.json
docs/
  product-specs/
    index.md
    feat-*.md
  exec-plans/
  references/
  golden-rules.md
```

Optional directories and files should only be created when they are useful for the project.

## Document Roles

| File | Purpose |
|---|---|
| `PRD.md` | Defines what is being built, for whom, and why. |
| `DESIGN.md` | Defines product look, feel, tokens, layout rules, and interaction principles. |
| `FRONTEND.md` | Defines UI architecture, routing, state, data fetching, and client behavior. |
| `TECH-SPEC.md` | Defines stack, dependencies, commands, environment, deployment, and constraints. |
| `ARCHITECTURE.md` | Defines system boundaries, data flow, dependency direction, and tradeoffs. |
| `docs/product-specs/` | Defines per-feature specs with observable acceptance steps. |
| `feature-list.json` | Tracks features in a machine-readable checklist. |
| `AGENTS.md` | Gives coding agents a concise entry point into the project. |
| `README.md` | Gives human developers project context and setup instructions. |

## Core Workflow

1. Establish product intent in `PRD.md`.
2. Translate product intent into concrete design rules in `DESIGN.md`.
3. Define frontend organization in `FRONTEND.md`.
4. Capture stack, commands, environment, and technical constraints in `TECH-SPEC.md`.
5. Define system boundaries and data flow in `ARCHITECTURE.md`.
6. Create one feature spec per feature under `docs/product-specs/`.
7. Mirror feature specs into `feature-list.json`.
8. Add `AGENTS.md` as the coding-agent navigation file.
9. Add or update the project `README.md` for human developers.

## Quality Bar

Generated documentation should be:

- Concise, structured, and easy for agents to parse.
- Traceable from product requirements to implementation guidance.
- Specific enough to reduce guesswork during coding.
- Verifiable through observable acceptance steps.
- Stored in versioned files instead of chat history.

Important rules:

- Keep each document focused on one responsibility.
- Avoid duplicating decisions across documents.
- Use stable feature IDs such as `FEAT-001`.
- Mark assumptions explicitly.
- Update downstream docs when upstream decisions change.
- Keep acceptance steps user-facing, not code-facing.

## Maintenance

Update `SKILL.md` when the workflow, generated document structure, or validation checklist changes.

Update this README when the skill's purpose, trigger cases, or expected outputs change.
