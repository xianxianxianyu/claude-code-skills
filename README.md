# SDD Dual-Mode Skeleton (SpecKit / OpenSpec)

This repository provides a Spec-Driven Development (SDD) team skeleton with two modes:

- SpecKit: best for greenfield / new modules / linear governance
- OpenSpec: best for incremental changes / multi-module work / strong auditability

All SDD artifacts are stored under `.claude/moyu/` (so the repo root stays clean).

## Layout

Repo root:

- `CLAUDE.md`: Plan Agent manual + path rules
- `.claude/`: subagents + templates (kept in place)

All SDD artifact roots:

- `.claude/moyu/specs/`      - SpecKit artifacts (one folder per WI)
- `.claude/moyu/openspec/`   - OpenSpec truth specs + change proposals
- `.claude/moyu/docs/`       - docs (development/architecture/requirements)
- `.claude/moyu/.specify/`   - Specify scaffolding (memory + templates)

## Quickstart

Read `CLAUDE.md` first (it is the workflow source of truth).

### 1) Create a Work Item (WI)

Naming: `WI-YYYYMMDD-###-slug`

Example: `WI-20260121-001-user-auth`

### 2) SpecKit mode (MODE=speckit)

1. Create folders:
   - `.claude/moyu/specs/<WI>/{slices,evidence}`
2. Copy templates:
   - `context.md`   <- `.claude/templates/common/context.md`
   - `spec.md`      <- `.claude/templates/speckit/spec.md`
   - `plan.md`      <- `.claude/templates/speckit/plan.md`
   - `tasks.md`     <- `.claude/templates/speckit/tasks.md`
   - `decisions.md` <- `.claude/templates/speckit/decisions.md`
3. Suggested orchestration (Plan Agent):
   - sdd-architect -> sdd-feasibility-analyst -> (human gate) -> sdd-strategic-planner
   - parallel sdd-implementer (by slices)
   - sdd-code-reviewer -> sdd-test-runner -> sdd-doc-sync

### 3) OpenSpec mode (MODE=openspec)

1. Create folders:
   - `.claude/moyu/openspec/changes/<WI>/{slices,evidence,specs}`
2. Copy templates:
   - `context.md`   <- `.claude/templates/common/context.md`
   - `proposal.md`  <- `.claude/templates/openspec/proposal.md`
   - `tasks.md`     <- `.claude/templates/openspec/tasks.md`
   - `decisions.md` <- `.claude/templates/openspec/decisions.md`
   - delta specs    <- `.claude/templates/openspec/delta-spec.md` (as needed)
3. Close-out (important):
   - After implementation + tests, merge final behavior back into:
     - `.claude/moyu/openspec/specs/**` (truth source)

## Subagents

Subagents live in `.claude/agents/` (kept in place), but all outputs must use `.claude/moyu/...` paths:

- sdd-architect: spec/proposal + delta specs (no coding)
- sdd-feasibility-analyst: options/decision/risks/rollback (write decisions)
- sdd-strategic-planner: tasks + slices + ownership matrix
- sdd-implementer: implement one slice only (strict touch list)
- sdd-code-reviewer: read-only review
- sdd-test-runner: test plan + tests + evidence
- sdd-doc-sync: docs close-out + spec truth consistency

## Rules (must follow)

- Never generate `specs/`, `openspec/`, `docs/`, or `.specify/` at repo root.
  All SDD artifacts must live under `.claude/moyu/`.
- Single source of truth:
  - SpecKit: `.claude/moyu/specs/<WI>/`
  - OpenSpec: `.claude/moyu/openspec/specs/**` (truth), `.claude/moyu/openspec/changes/<WI>/` (proposal)
- Evidence-first: write commands and result summaries into `ARTIFACT_ROOT/evidence/`.

## License

Add a `LICENSE` file (e.g. MIT / Apache-2.0) if you plan to publish this as an open source project.

