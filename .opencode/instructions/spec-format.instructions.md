# Spec Format Instructions

When working with specs in this repo, follow these conventions.

## Spec Location

All specs live in `specs/`. The directory structure mirrors the module structure:

```
specs/
  architecture.md
  style-guide.md
  <module>/
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

## Data Layout
Struct definitions, sizes, alignments.
Can be C-style or prose — both are valid.

## Behavior
Pseudocode or prose for each function.
Precise enough to be unambiguous.
Loose enough to not be literal C code.

## Ownership
Who owns resources created by this module.
When they are released. Dependency ordering.

## Error Handling
What happens when things go wrong.

## Tradeoffs
Performance, alternatives, scaling considerations.

## Output Files
- src/module/file.h
- src/module/file.c
```

## Style

- **Prose-first**: Write like a book chapter, not a pseudocode listing
- **Document the obvious**: Even trivial operations should be spelled out
- **Declare ownership**: Every resource must have a clear owner and release strategy
- **Consider tradeoffs**: What happens at 10x or 100x scale?

## Markers

- `<!-- agent-verified -->` — Formula or detail inserted by the agent after a successful completeness gate
- `<!-- tradeoff-acknowledged -->` — Tradeoff discussion captured during gate dialogue

These markers indicate verified content that won't be re-gated on subsequent passes.
