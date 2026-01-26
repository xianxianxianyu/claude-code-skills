# SDD Pack Architecture

## Overview

The SDD (Spec-Driven Development) pack provides a dual-mode workflow for specification-driven development:

- **SpecKit**: For greenfield work, new modules, linear governance
- **OpenSpec**: For incremental changes, multi-module work, auditability

## Directory Structure

```
.claude/
├── CLAUDE.md                    # Project-level config (slim)
├── agents/                      # Agent definitions
│   ├── sdd-architect.md         # Spec/proposal design
│   ├── sdd-feasibility-analyst.md
│   ├── sdd-strategic-planner.md
│   ├── sdd-implementer.md
│   ├── sdd-code-reviewer.md
│   ├── sdd-test-runner.md
│   └── sdd-doc-sync.md
├── skills/                      # Skill definitions
│   ├── sdd-common/SKILL.md
│   └── sdd-*/SKILL.md
├── rules/                       # Auto-loaded rules
│   └── dual-sdd/
│       ├── docs.md              # Documentation rules
│       ├── testing.md           # Testing rules
│       ├── style.md             # Code style rules
│       ├── security.md          # Security rules
│       └── docs/                # Path-scoped rules
│           ├── prd.md           # For spec.md/proposal.md
│           └── feasibility.md   # For decisions.md
└── moyu/                        # Artifact storage
    ├── specs/                   # SpecKit artifacts
    ├── openspec/                # OpenSpec system
    │   ├── changes/             # Change proposals
    │   └── specs/               # Truth specs
    ├── templates/               # Canonical templates
    ├── docs/                    # Development docs
    └── trace/                   # Trace logs
```

## Rules Auto-Loading

Rules in `.claude/rules/dual-sdd/` are automatically loaded by Claude Code. Path-scoped rules in `docs/` subdirectory apply to specific file patterns:

- `docs/prd.md` → applies to `**/spec.md`, `**/proposal.md`
- `docs/feasibility.md` → applies to `**/decisions.md`

## Agent Pipeline

```
Phase A: Specification (serial + human gate)
  sdd-architect → sdd-feasibility-analyst → sdd-strategic-planner

Phase B: Implementation (parallelizable)
  sdd-implementer → sdd-code-reviewer → sdd-test-runner

Phase C: Documentation
  sdd-doc-sync
```

## Agent-Skill Mapping

Each agent declares skills via frontmatter `skills:` field:

| Agent | Skills |
|-------|--------|
| sdd-architect | sdd-common, sdd-architect |
| sdd-feasibility-analyst | sdd-common, sdd-feasibility |
| sdd-strategic-planner | sdd-common, sdd-planner |
| sdd-implementer | sdd-common, sdd-implementer |
| sdd-code-reviewer | sdd-common, sdd-reviewer |
| sdd-test-runner | sdd-common, sdd-tester |
| sdd-doc-sync | sdd-common, sdd-docsync |
