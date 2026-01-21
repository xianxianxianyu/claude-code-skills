# SDD Dual-Mode Skeleton (SpecKit / OpenSpec)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

A Spec-Driven Development (SDD) scaffold for Claude Code/LLM teams. It supports two modes:

- SpecKit: best for greenfield work, new modules, or linear governance
- OpenSpec: best for incremental changes, multi-module work, and auditability

All SDD artifacts live under `.claude/moyu/` so the repo root stays clean.

## Why this repo

- Single source of truth per Work Item (WI)
- Evidence-first development (commands + results)
- Deterministic artifact locations for fast reviews
- Small, reviewable slices to reduce risk
- Context pack discipline for token efficiency

## Quickstart

1) Read `CLAUDE.md` (workflow source of truth).
2) Create a Work Item (WI):
   - Format: `WI-YYYYMMDD-###-slug`
   - Example: `WI-20260121-001-user-auth`
3) Choose a mode:
   - SpecKit (MODE=speckit)
   - OpenSpec (MODE=openspec)
4) Copy templates and run subagents as needed.
5) Close out by updating the spec truth source and docs.

## Repository layout

- `CLAUDE.md`: Plan Agent manual + path rules
- `.claude/agents/`: subagent system prompts
- `.claude/templates/`: shared templates
- `.claude/moyu/specs/`: SpecKit artifacts (one folder per WI)
- `.claude/moyu/openspec/`: OpenSpec truth specs + change proposals
- `.claude/moyu/docs/`: development/architecture/requirements docs
- `.claude/moyu/.specify/`: Specify scaffolding (memory + templates)

## Mode details

### SpecKit (MODE=speckit)

1. Create folders:
   - `.claude/moyu/specs/<WI>/{slices,evidence}`
2. Copy templates:
   - `context.md`   <- `.claude/templates/common/context.md`
   - `spec.md`      <- `.claude/templates/speckit/spec.md`
   - `plan.md`      <- `.claude/templates/speckit/plan.md`
   - `tasks.md`     <- `.claude/templates/speckit/tasks.md`
   - `decisions.md` <- `.claude/templates/speckit/decisions.md`
3. Suggested orchestration:
   - sdd-architect -> sdd-feasibility-analyst -> (human gate) -> sdd-strategic-planner
   - parallel sdd-implementer (by slices)
   - sdd-code-reviewer -> sdd-test-runner -> sdd-doc-sync

### OpenSpec (MODE=openspec)

1. Create folders:
   - `.claude/moyu/openspec/changes/<WI>/{slices,evidence,specs}`
2. Copy templates:
   - `context.md`   <- `.claude/templates/common/context.md`
   - `proposal.md`  <- `.claude/templates/openspec/proposal.md`
   - `tasks.md`     <- `.claude/templates/openspec/tasks.md`
   - `decisions.md` <- `.claude/templates/openspec/decisions.md`
   - delta specs    <- `.claude/templates/openspec/delta-spec.md` (as needed)
3. Close-out (important):
   - After implementation + tests, merge final behavior into `.claude/moyu/openspec/specs/**`

## Subagents

- sdd-architect: spec/proposal + delta specs (no coding)
- sdd-feasibility-analyst: options/decision/risks/rollback (write decisions)
- sdd-strategic-planner: tasks + slices + ownership matrix
- sdd-implementer: implement one slice only (strict touch list)
- sdd-code-reviewer: read-only review
- sdd-test-runner: test plan + tests + evidence
- sdd-doc-sync: docs close-out + spec truth consistency

## Rules (must follow)

- Never generate `specs/`, `openspec/`, `docs/`, or `.specify/` at repo root.
- All SDD artifacts must live under `.claude/moyu/`.
- Single source of truth per WI:
  - SpecKit: `.claude/moyu/specs/<WI>/`
  - OpenSpec: `.claude/moyu/openspec/specs/**` (truth), `.claude/moyu/openspec/changes/<WI>/` (proposal)
- Evidence-first: write commands and result summaries into `ARTIFACT_ROOT/evidence/`.

## Contributing

Issues and PRs are welcome. Keep changes small, focused, and consistent with the workflow rules in `CLAUDE.md`.

## License

Add a `LICENSE` file (MIT/Apache-2.0) if you plan to publish this project.
