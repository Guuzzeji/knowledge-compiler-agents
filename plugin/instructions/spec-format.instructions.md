# Spec Format Instructions

When working with specs in this repo, follow these conventions.

## Spec Location

All specs live in `.kc-specs/`. The directory structure mirrors the module structure:

```
.kc-specs/
  architecture.md
  style-guide.md
  <domain>/
    <component>.md
```

## Spec Structure

Each spec reads like a book chapter. The general structure is:

```markdown
# Module Name

## Purpose

What this module does and why it exists.

## Dependencies

Which other modules/specs this depends on.

## Data Model

Core entities, fields, constraints, and relationships.
Use Mermaid diagrams, structured tables, or prose as appropriate.

## Behavior

Pseudocode or prose for major workflows, APIs, or operations.
Precise enough to be unambiguous.
Implementation-language details are optional unless required.

## Ownership

Who is responsible for resources, state, and lifecycle boundaries.
When resources are created, transferred, and released.

## Error Handling

What happens when things go wrong.

## Tradeoffs

Performance, alternatives, scaling considerations.

## Output Files

- src/domain/component.ext
- tests/domain/component.test.ext
```

## Style

- **Prose-first**: Write like a book chapter, not a pseudocode listing
- **Document the obvious**: Even trivial operations should be spelled out
- **Declare ownership**: Every resource or stateful boundary must have a clear owner and lifecycle strategy
- **Consider tradeoffs**: What happens at 10x or 100x scale?
- **Diagrams**: Use Mermaid syntax only for all diagrams

## Markers

- `<!-- agent-verified -->` — Formula or detail inserted by the agent after a successful completeness gate
- `<!-- tradeoff-acknowledged -->` — Tradeoff discussion captured during gate dialogue

These markers indicate verified content that won't be re-gated on subsequent passes.
