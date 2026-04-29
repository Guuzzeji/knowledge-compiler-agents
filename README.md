# knowledge-compiler-agents

Spec-first agent templates and instructions for building software with GitHub Copilot.

## Purpose

This project provides a reusable, spec-driven workflow so teams can:

- write requirements before implementation
- validate specs with structured quality gates
- generate code from validated specs with less ambiguity
- keep human intent and generated output aligned

In short: specs are the source of truth, and code is a derived artifact.

## Install (Github Copilot Plugin)

```bash
copilot plugin marketplace add Guuzzeji/knowledge-compiler-agents
copilot plugin install kc-agents@knowledge-compiler-agents-marketplace
```

## Typical Workflow

1. Initialize context with `agents/spec-init-project.md`.
2. Build or refresh conventions with `agents/style-guide-builder.md`.
3. Draft or expand specs with `agents/spec-author.md`.
4. Run quality gates with the gate agents:
   - `spec-lint`
   - `spec-gate-correctness`
   - `spec-gate-completeness`
   - `spec-gate-tradeoffs`
   - `spec-gate-depth`
5. Orchestrate generation with `agents/spec-engine.md`.
6. Validate generated output with `agents/spec-build.md`.

## Agent Reference (Detailed)

### `agents/spec-init-project.md`

Purpose:

- Bootstraps a repository into spec-first workflow mode.
- Interviews the user for project fundamentals (name, goals, runtime, constraints, module map).
- Creates or updates `project.md` as canonical high-level context.

What it produces:

- Required: `project.md` with purpose, goals, architecture summary, spec structure, workflow, constraints.
- Recommended baseline spec files if missing: `.kc-specs/architecture.md` and `.kc-specs/style-guide.md`.
- Workflow handoff guidance that points agents to project and instruction files first.

Use this when:

- Starting a new repo.
- Migrating an existing codebase to spec-driven development.

### `agents/style-guide-builder.md`

Purpose:

- Co-authors a concrete, enforceable style guide via interview.
- Converts vague preferences into reviewable must/should/may rules.

What it enforces:

- Explicit language feature policy, naming, formatting, ownership/lifecycle, API design, testing expectations.
- Practical banned-pattern list with rationale.
- Exception process with an approval owner.

Use this when:

- You need a first canonical style guide.
- Existing conventions are inconsistent or not enforceable.

### `agents/spec-author.md`

Purpose:

- Interview-style spec co-author that turns human explanations into full spec prose.
- Applies knowledge-gating during authoring so design decisions are explicit before code generation.

What it does:

- Builds a section plan, dependency order, and conversation flow first.
- Asks one focused question at a time, including "why" behind design choices.
- Drafts prose-first sections and iterates with the human.
- Uses `<!-- agent-verified -->` when the agent provides missing details after validation.

Use this when:

- Creating a new spec from scratch.
- Expanding incomplete sections in an existing spec.

### `agents/spec-lint.md` (Gate 0)

Purpose:

- Fast structural pre-check before deeper technical gates.

What it checks:

- Required sections exist.
- Dependency references are valid.
- Output file declarations are present and non-conflicting.
- Thin sections, ownership discussion presence, stale markers, basic naming checks.

Outcome:

- Blocks only on structural blockers.
- Emits warnings for shallow or suspicious sections.

### `agents/spec-gate-correctness.md` (Gate 1)

Purpose:

- Technical correctness gate.

What it checks:

- Wrong math, contradictions, impossible claims.
- API/dependency misuse and type mismatch in claims.

Outcome:

- Binary: any error blocks.

### `agents/spec-gate-completeness.md` (Gate 2)

Purpose:

- Finds concepts referenced but not defined.

What it checks:

- Missing definitions behind terms/patterns that affect implementation.
- Ownership and lifecycle declarations (always gated when resources exist).

Outcome:

- Interactive quiz flow with one question at a time.
- Verified answers are inserted and tagged with `<!-- agent-verified -->`.

### `agents/spec-gate-tradeoffs.md` (Gate 3)

Purpose:

- Advisory tradeoff analysis.

What it checks:

- Performance hotspots, scaling constraints, failure modes, over-engineering risks.

Outcome:

- Does not hard-block.
- Produces actionable flags for human decision.

### `agents/spec-gate-depth.md` (Gate 4)

Purpose:

- Ambiguity/depth gate using the two-engineer test.

What it checks:

- Unnamed architectural decisions.
- Named-but-undescribed behaviors.
- Happy-path-only specs.
- Incomplete lifecycle definitions.

Outcome:

- Blocks if two competent engineers could produce materially different implementations from the same spec.

### `agents/spec-reviewer.md`

Purpose:

- Holistic spec critique beyond gate mechanics.

What it reviews:

- Internal contradictions.
- Cross-spec compatibility.
- Implicit assumptions.
- Design quality and maintainability risks.

Outcome:

- Severity-ranked findings (blockers/warnings/suggestions) for human revision.

### `agents/spec-engine.md`

Purpose:

- Main orchestrator of the full spec-to-code pipeline.

What it does:

- Runs/delegates gates in dependency-aware order.
- Enforces clean-room generation and literal generation rules.
- Generates only declared output files from validated specs.
- Emits `TODO(spec)` for missing requirements instead of inventing behavior.
- Maintains per-spec gate cache and invalidation logic.
- Delegates build verification to `spec-build`.

Outcome:

- Code generation only after gates pass.

### `agents/spec-build.md`

Purpose:

- Post-generation build verification and code-level stabilization.

What it does:

- Runs canonical build command(s), classifies failures, and fixes generated code issues.
- Preserves provenance headers and marks edits with `build-fix:` comments.
- Reports spec gaps back to the spec loop instead of patching specs directly.

Outcome:

- Build success or clear, actionable failure/spec-gap report.

## Template File Reference (Detailed)

### `instructions/spec-format.instructions.md`

Purpose:

- Defines canonical spec structure, location, and writing conventions.

Key rules:

- Specs live under `.kc-specs/`.
- Use prose-first chapter style.
- Include Purpose, Dependencies, behavior/model sections, ownership, errors, tradeoffs, and output files.
- Use Mermaid for diagrams.
- Supports markers like `<!-- agent-verified -->` and `<!-- tradeoff-acknowledged -->`.

### `instructions/style-guide.instructions.md`

Purpose:

- Defines how to author and review a high-quality project style guide.

Key rules:

- Provides required section template from project identity through change management.
- Requires normative language (must/should/may), concrete constraints, rationale for bans, examples, ownership rules, and enforcement expectations.
- Includes completeness and consistency checks to prevent contradictory guidance.

### `copilot-instructions.md`

Purpose:

- Repository-level operating rules for Copilot behavior in this project.

Role in workflow:

- Ensures contributors and agents follow the same spec-first operating model.
- Defines read order and gate/generation sequencing constraints.

## Notes

- This repository is a workflow/template pack, not an application runtime.
- It is designed to work best in repositories that keep specs under `.kc-specs/`.
- Keep instructions and agent files versioned with your project so collaborators and Copilot share the same context.
