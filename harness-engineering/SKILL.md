---
name: harness-engineering
description: Build or update a Harness Engineering knowledge base from a PRD, product idea, or existing project plan. Use when you needs to generate agent-ready project documentation, including PRD.md, DESIGN.md, FRONTEND.md, TECH-SPEC.md, ARCHITECTURE.md, docs/product-specs/, feature-list.json, AGENTS.md, README.md, or when a project needs structured feature specifications, acceptance criteria, implementation guidance, or AI handoff documentation.
---

# Harness Engineering

Transform a PRD or rough product idea into a complete, agent-ready engineering knowledge base. The output should let Codex or another coding agent implement features without guessing product intent, design rules, architecture boundaries, or acceptance criteria.

## Core Principles

1. Keep each document responsible for one layer of decision-making.
2. Preserve traceability from product intent to design, architecture, feature specs, and implementation tasks.
3. Write for agents first: concise, explicit, structured, and easy to parse.
4. Make every feature verifiable through observable user-facing acceptance steps.
5. Store decisions in versioned project files, not in chat history or external tools.

## Required Inputs

Use the best available source:

- A complete PRD.
- A rough product idea that can be expanded into a PRD.
- Existing project documents that need restructuring into the Harness format.

If important product or technical details are missing, make conservative assumptions, mark them clearly, and continue unless the missing information would make the output misleading.

## Output Structure

Create or update this structure at the project root:

```text
project-root/
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

Only create optional directories or files when they are useful for the project.

## Document Responsibilities

| Document | Primary question | Main audience | Source of truth |
|---|---|---|---|
| `PRD.md` | What are we building, for whom, and why? | Product and engineering | User input |
| `DESIGN.md` | What should the product feel and look like? | Design and frontend | `PRD.md` |
| `FRONTEND.md` | How should UI, routing, state, and client behavior be organized? | Frontend engineers | `PRD.md`, `DESIGN.md` |
| `TECH-SPEC.md` | What stack, dependencies, build process, and technical constraints apply? | Full-stack engineers | `PRD.md`, `FRONTEND.md` |
| `ARCHITECTURE.md` | How is the system divided, how does data flow, and what boundaries are enforced? | Architects and agents | `TECH-SPEC.md`, `FRONTEND.md` |
| `docs/product-specs/` | How is each feature verified? | Implementing agents and QA | `PRD.md` |
| `feature-list.json` | What features exist and what is complete? | Project tracking agents | `docs/product-specs/` |
| `AGENTS.md` | Where should agents start? | Coding agents | All core documents |
| `README.md` | How does a human understand and run the project? | Developers and users | Project state |

## Workflow

### 1. Establish Product Intent

Create or refine `PRD.md`. Include:

- Product positioning and one-sentence value proposition.
- Target users and primary use cases.
- Competitor or reference-product summary when relevant.
- Feature modules grouped by user tier or release phase.
- Core user journeys.
- UX strategy and trust-building requirements.
- Monetization model when relevant.
- Success metrics.

Keep the PRD actionable. Avoid long market essays unless they directly affect scope or implementation.

### 2. Define Design Rules

Create `DESIGN.md` from the PRD's UX direction. Include:

- Design philosophy in 3-5 concrete keywords.
- Reference products or visual anchors when useful.
- Color system with implementation-ready tokens.
- Typography scale.
- Spacing system.
- Motion and interaction rules.
- Responsive breakpoints.
- Component-level styling requirements for critical surfaces.

Make design decisions specific enough that a frontend agent can implement them without inventing a visual system.

### 3. Define Frontend Architecture

Create `FRONTEND.md` from `DESIGN.md` and the PRD feature modules. Include:

- Component hierarchy.
- Directory organization.
- Routing model.
- State management approach.
- Data-fetching conventions.
- Error, empty, loading, and permission states.
- Performance requirements.
- Accessibility requirements.

Use the project's existing framework conventions when updating an existing codebase.

### 4. Define Technical Specification

Create `TECH-SPEC.md` from the frontend plan and product constraints. Include:

- Stack overview with versions when known.
- Core dependencies and installation commands.
- Development environment requirements.
- Directory conventions.
- Build, test, and deployment commands.
- Environment variables.
- Performance targets.
- Security and privacy constraints.

Every technical choice should support a stated product or architecture need.

### 5. Define System Architecture

Create `ARCHITECTURE.md` from `TECH-SPEC.md` and `FRONTEND.md`. Include:

- System overview diagram in ASCII when useful.
- Domain boundaries and module responsibilities.
- Allowed dependency direction.
- Data flow for critical user journeys.
- Integration boundaries.
- State ownership rules.
- Architecture decision records for meaningful tradeoffs.
- Forbidden patterns and recommended alternatives.

Record tradeoffs, not obvious defaults. An ADR should explain why one reasonable option was chosen over another.

### 6. Create Feature Specifications

Create `docs/product-specs/index.md` and one `feat-*.md` file per feature.

Use kebab-case filenames:

```text
docs/product-specs/feat-{feature-name}.md
```

Each feature spec should include:

```markdown
# FEAT-001: Feature Name

One-sentence value statement.

## User Story
- As a [user type], I want [action], so that [benefit].

## Acceptance Steps
1. Observable user-facing step.
2. Include expected result.
3. Cover normal, edge, and failure paths.

## UI/UX Requirements
- Reference relevant design tokens, layout rules, and component behavior.

## Technical Notes
- Mention relevant modules, APIs, algorithms, or constraints.

## Related Files
- `components/...`
- `hooks/...`
- `lib/...`

## Edge Cases
| Scenario | Expected behavior |
|---|---|
| Example failure case | Expected recovery |
```

Acceptance steps must be verifiable from the user's perspective. Put implementation details in `Technical Notes`, not in the acceptance steps.

### 7. Create Feature Tracking

Create `feature-list.json` as a machine-readable checklist:

```json
[
  {
    "id": "FEAT-001",
    "name": "Feature name",
    "category": "functional",
    "phase": "mvp-v0.1",
    "tier": "all",
    "priority": "p0",
    "description": "One-sentence description.",
    "spec_path": "docs/product-specs/feat-feature-name.md",
    "steps": [
      "Acceptance step 1",
      "Acceptance step 2"
    ],
    "passes": false
  }
]
```

Use these field values unless the project defines its own taxonomy:

- `category`: `functional`, `ux`, `marketing`, `technical`, or `infrastructure`.
- `phase`: `mvp-v0.1`, `mvp-v0.2`, `pro-v1.0`, or `growth`.
- `tier`: `free`, `pro`, or `all`.
- `priority`: `p0`, `p1`, `p2`, or `p3`.
- `passes`: `false` until the feature has been implemented and verified.

### 8. Create Agent Entry Point

Create `AGENTS.md` as a concise navigation file. Keep it under 100 lines when possible.

Include:

- Project summary.
- Stack summary.
- Knowledge-base map.
- Current active plan location.
- Standard implementation workflow.
- Documentation update rules.
- Escalation marker for uncertainty, such as `@review`.

`AGENTS.md` is a map, not a tutorial. Link to source documents instead of duplicating them.

### 9. Create Human Entry Point

Create `README.md` for human developers. Include:

- Project overview.
- Screenshot or product context when available.
- Tech stack.
- Directory map.
- Local setup commands.
- Build, test, and deployment commands.
- Important links or references.

## Validation Checklist

Before finishing, verify:

- Every PRD feature module has a matching feature spec.
- Every `feature-list.json` item has a real `spec_path`.
- Design tokens in `DESIGN.md` are referenced by `FRONTEND.md`.
- Frontend structure in `FRONTEND.md` is compatible with `TECH-SPEC.md`.
- Technical choices in `TECH-SPEC.md` support the PRD requirements.
- Architecture boundaries in `ARCHITECTURE.md` are implementable in the selected stack.
- Feature acceptance steps are observable and testable.
- `AGENTS.md` links to all core documents without duplicating them.
- Optional `docs/golden-rules.md` is referenced from `AGENTS.md` if created.

## Quality Rules

- Prefer concrete tables, checklists, and short sections over long prose.
- Keep each document focused on its responsibility.
- Avoid duplicating the same decision across documents; link to the source of truth.
- Mark assumptions explicitly.
- Keep examples project-specific.
- Update downstream documents when an upstream decision changes.
- Use stable IDs such as `FEAT-001` for cross-document references.

## Common Fixes

### Overlong Documents

Move feature-level detail into `docs/product-specs/`. Keep core documents readable and navigable.

### Inconsistent Decisions

Trace the decision chain from `PRD.md` to downstream documents and update every affected file.

### Code-Level Acceptance Steps

Rewrite acceptance steps as user-observable behavior. Move code details to `Technical Notes`.

### Missing Edge Cases

Add failure, cancellation, empty state, permission, limit, and recovery scenarios to each feature spec.

### Stale Architecture

Update `ARCHITECTURE.md`, `TECH-SPEC.md`, and affected feature specs whenever system boundaries or major dependencies change.
