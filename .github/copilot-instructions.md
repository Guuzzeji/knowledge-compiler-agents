# Spec-Driven Workflow Instructions

This repository uses a spec-driven development model.

Always treat specs as the source of truth. Implementation code is a derived artifact.

## Read Order

Before making decisions, read files in this order:

1. project.md for project purpose, goals, and high-level structure.
2. .kc-specs/architecture.md for system boundaries and module map.
3. .kc-specs/style-guide.md for coding rules and naming conventions.
4. Relevant specs under .kc-specs/ for feature-level behavior.

## Standard Workflow

Use this pipeline for all feature work:

1. Spec: Author or update prose specs in .kc-specs/.
2. Validate: Run the gate flow (lint, correctness, completeness, tradeoffs, depth).
3. Generate: Produce code only from validated specs.
4. Review: Inspect generated code and run build verification.

If a gate fails, stop generation and update the spec first.

## Validation Model

- Gate 0: Lint and structure checks.
- Gate 1: Technical correctness.
- Gate 2: Completeness and missing definitions.
- Gate 3: Tradeoffs and scaling considerations.
- Gate 4: Depth and ambiguity resolution.

Gates 1-3 may run in parallel after Gate 0 passes.
Gate 4 should run after Gates 1-2 are resolved.

## Agent Coordination

- spec-init-project initializes project context and baseline docs.
- spec-author co-authors specs from user explanations.
- spec-engine orchestrates gate validation and generation.
- spec-reviewer provides holistic spec quality review.
- spec-build verifies build output and fixes generated-code build issues.

## Rules

- Do not generate code from unvalidated specs.
- Do not add behavior not described in specs.
- Prefer TODO(spec) comments for missing requirements instead of assumptions.
- Keep docs and generated output aligned with .kc-specs/style-guide.md.

## Canonical Context File

project.md is the canonical high-level project context file for both humans and agents.
When project purpose, scope, or goals change, update project.md first, then update dependent specs.
