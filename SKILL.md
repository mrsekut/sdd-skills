---
name: sdd
description: Spec-driven development workflow for implementing features with structured documentation. Use when starting a new feature, task, or implementation that benefits from upfront planning. Triggers: "/sdd", "spec-driven", "create spec", "implementation plan", or when user describes a feature/task to implement.
---

# SDD - Spec Driven Development

A structured workflow for implementing features through documentation-first development.

## Directory Setup

Create spec directory for the task:

```bash
mkdir -p ./.specs/{task-name}
```

Name `{task-name}` based on the task (e.g., `create-article-component`, `add-user-auth`).

## Phase Overview

```
1. Context Analysis    → 1-context.md
2. Requirements        → 2-requirements.md
3. Design              → 3-design.md
4. Implementation Plan → 4-implementation-plan-{N}.md
5. Implementation      → (PR loop)
```

Each phase: Create document → Present to user → Get approval → Next phase

## Phase 1: Context Analysis

Analyze the existing codebase to understand patterns and constraints.

Create `.specs/{task-name}/1-context.md`. See [references/templates.md](references/templates.md#1-context) for format.

Contents:

- Tech stack and frameworks
- Relevant existing code/components
- Project conventions (naming, structure)
- Constraints or limitations

Present to user and get approval before proceeding.

## Phase 2: Requirements Definition

Define WHAT the task should accomplish, not HOW.

Create `.specs/{task-name}/2-requirements.md`. See [references/templates.md](references/templates.md#2-requirements) for format.

Guidelines:

- Use user story format
- List acceptance criteria as checkboxes
- Define scope boundaries (in/out of scope)
- Keep concise: max 5 items per section
- No technical implementation details

Present to user and get approval before proceeding.

## Phase 3: Design

Define the implementation direction at an architectural level. Not implementation details.

Create `.specs/{task-name}/3-design.md`. See [references/templates.md](references/templates.md#3-design) for format.

Contents:

- **Domain Models**: Core type definitions only (not utility types or internal details)
- **Feature Boundaries**: What features exist, their responsibilities (1 line each), dependencies between them
- **Directory Structure**: Feature-level package structure only (not detailed files within each feature)
- **Main Flow**: Key processing steps with data transformation (e.g., `validateInput: FormInput → ValidatedInput`)
- **Layer Structure**: Where each logic belongs in the project's layer hierarchy

### Design Principle: Push Logic to Core

Write core logic first, independent of framework or infrastructure. The core should not know whether it's used by React, CLI, server, etc.

Every project has a layer hierarchy (inner = more pure, outer = more side-effectful). Always push logic as far inward as possible.

Example (React project):

```
Core (pure functions) → State (jotai) → Hooks → Components
```

Example (Backend project):

```
Domain Logic → Application Service → Controller → HTTP Handler
```

Identify your project's layers and document where each logic belongs. Benefits: easier testing, better reusability, clearer boundaries.

Present to user and get approval before proceeding.

## Phase 4: Implementation Plan

Break down the design into PR-sized units.

Create `.specs/{task-name}/4-implementation-plan-{N}.md` for each PR. See [references/templates.md](references/templates.md#4-implementation-plan) for format.

### PR Structure Strategy

Choose based on task characteristics:

- **Vertical (by feature)**: Slice through all layers for one feature. Preferred when features are independent and early feedback is valuable.
- **Horizontal (by layer)**: Build one layer at a time. Use when core design needs to be solid before building on top.

### Guidelines

- One file per PR
- PR unit = reviewable size
- Each PR must define how it will be reviewed (tests, types, working UI, etc.)
- Include checkbox tasks for progress tracking
- Show task dependencies (what can run in parallel)
- Commits are suggestions, adjust during implementation

Present all plans to user and get approval before proceeding.

## Phase 5: Implementation

Execute implementation plans PR by PR.

### PR Loop

For each `4-implementation-plan-{N}.md`:

```
1. Execute tasks (check boxes as you go)
2. Suggest commit messages (do NOT run git commands)
3. Run verification: tsc, lint, test
4. Check: Do learnings require updates to 2-requirements.md or 3-design.md?
   - Yes → Update documents, review impact on remaining plans
   - No → Continue
5. Present to user for approval
6. User OK → Next PR
   User NG → Address feedback, repeat from step 3
```

### Important Rules

- Follow 2-requirements.md and 3-design.md strictly
- Update specs directly when learnings emerge (no separate learnings file)
- Suggest commit messages but never execute git commands
- Run `tsc`/`lint`/`test` before user confirmation
