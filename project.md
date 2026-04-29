# Project Overview

## Project Name

knowledge-compiler-agents

## Purpose

This repository defines a reusable, spec-driven workflow for building software through structured specification documents and agent-assisted generation.

The goal is to make specs the source of truth, keep implementation behavior aligned with prose requirements, and support consistent collaboration between humans and agents.

## Goals

- Establish a clear spec-first workflow for new and existing projects.
- Define a repeatable validation pipeline before code generation.
- Keep code generation deterministic and traceable to spec documents.
- Make project context easy for agents and contributors to discover.
- Reduce ambiguity by documenting architecture, ownership, and expected outputs.

## Spec Structure

The canonical specification layout is under .kc-specs/:

- .kc-specs/architecture.md: system architecture, module map, and boundaries.
- .kc-specs/style-guide.md: coding conventions and implementation constraints.
- .kc-specs/<domain>/<component>.md: module-level behavior, ownership, and output files.

Each spec should follow the repo spec format instructions and include at least:

- Purpose
- Dependencies
- Behavior and data model details
- Ownership
- Output Files

## Workflow

The standard development workflow is:

1. Author or update specs in .kc-specs/.
2. Run validation gates (lint, correctness, completeness, tradeoffs, depth).
3. Generate code only from validated specs.
4. Review generated code and run build verification.

## Project Context For Agents

Agents should treat this file as the high-level source for:

- Project purpose and goals
- Spec folder organization
- Expected workflow and pipeline order

Detailed implementation and formatting rules remain in:

- .github/copilot-instructions.md
- .github/instructions/spec-format.instructions.md
- .github/instructions/style-guide.instructions.md

## Current Status

This file is intentionally generic and can be extended for each new project that adopts the spec-driven process.
