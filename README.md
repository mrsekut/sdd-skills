# SDD Skills

A Claude Code skill for Spec-Driven Development (SDD).

## Overview

Provides a structured workflow for documentation-first feature implementation. By clarifying specifications upfront, it reduces rework and enables implementation in reviewable units.

## Usage

Invoke in Claude Code:

```
/sdd implement article posting feature
```

## Workflow

Consists of 5 phases:

```
1. Context Analysis    → 1-context.md
2. Requirements        → 2-requirements.md
3. Design              → 3-design.md
4. Implementation Plan → 4-implementation-plan-{N}.md
5. Implementation      → (PR loop)
```

Each phase creates a document, gets user approval, then proceeds to the next.

## License

MIT
