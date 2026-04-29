# Style Guide Instructions

When creating or updating a style guide in this repo, follow these conventions.

## Style Guide Location

Use one canonical file path for the project style guide:

- Preferred: `style-guide.md`
- Alternate (spec-driven repos): `.kc-specs/style-guide.md`

If both exist, document which one is authoritative and keep rules synchronized.

## Style Guide Purpose

The style guide is the source of truth for coding conventions and implementation constraints.
It must be specific enough that two engineers (or agents) would produce consistent code decisions.

## Required Structure

Write the guide using this template structure:

```markdown
# Style Guide

## Project Identity

## Guiding Principles

## Scope Of This Guide

## Language Feature Policy

### Preferred

### Restricted

### Forbidden

## Dependency Policy

## File Organization And Module Boundaries

## Naming Conventions

## Formatting And Layout Rules

### Canonical Formatting Example

## API And Function Design

## Data Ownership And Lifetime

## Error Handling And Diagnostics

## Concurrency And Thread Safety

## Testing And Verification Expectations

## Documentation Expectations

## Banned Patterns And Anti-Patterns

## Exceptions Process

## Change Management

## Style Guide Checklist
```

## Writing Rules

- **Rule-first language**: Use clear normative wording such as must, must not, should, and may.
- **Concrete over vague**: Replace subjective phrases with explicit constraints and examples.
- **Reason when banning**: Every forbidden feature or pattern must include a short rationale.
- **Show examples**: Include at least one canonical formatting and API example.
- **Define ownership**: State lifecycle and ownership rules for resources and state.
- **State enforcement**: Explain how the guide is enforced (review checklist, lints, CI, etc).

## Completeness Standard

A style guide is complete only when:

- Naming, formatting, and API contracts are unambiguous
- Dependency and language feature policies are explicit
- Error handling and ownership rules are actionable
- Exceptions process exists and identifies who approves deviations

## Consistency Requirements

- New rules must not conflict with earlier sections
- If a rule changes, update examples and checklist items in the same edit
- Keep terminology stable across sections (for example, do not switch between "module" and "component" without defining both)

## Review Guidance

When reviewing style-guide changes, prioritize:

1. Ambiguity that could produce inconsistent implementations
2. Missing constraints around ownership, errors, and API behavior
3. Internal contradictions between sections
4. Overly broad bans without rationale or exception process
