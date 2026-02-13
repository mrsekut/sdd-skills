# SDD Skills

A Claude Code skill for Spec-Driven Development (SDD).

## Installation

```
npx skills add mrsekut/sdd-skills
```

## Overview

Provides a structured workflow for documentation-first feature implementation. By clarifying specifications upfront, it reduces rework and enables implementation in reviewable units.

## Usage

Invoke in Claude Code:

```
/sdd implement article posting feature
```

## Workflow

Consists of 6 phases:

```
1. Context Analysis    → 1-context.md
2. Prototyping (opt)   → 2-prototyping-learnings.md
3. Requirements        → 3-requirements.md
4. Design              → 4-design.md
5. Implementation Plan → 5-implementation-plan-{N}.md
6. Implementation      → (PR loop)
```

Each phase creates a document, gets user approval, then proceeds to the next.

## License

MIT
