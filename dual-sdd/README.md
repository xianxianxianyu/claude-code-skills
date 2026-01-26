# Moyu Dual SDD Scaffold (SpecKit / OpenSpec)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Read this in Chinese: [`README.zh-CN.md`](README.zh-CN.md)

A Spec-Driven Development (SDD) scaffold for Claude Code with dual-mode workflow:

- **SpecKit**: Greenfield work, new modules, linear governance
- **OpenSpec**: Incremental changes, multi-module work, auditability

## Features

- Dual SDD modes with single-source-of-truth rule per Work Item (WI)
- Standard Claude Code structure: agents in `.claude/agents/`, skills in `.claude/skills/`
- **Auto-loaded rules** in `.claude/rules/dual-sdd/` for consistent policies
- Deterministic artifact paths under `.claude/moyu/`
- Shared templates for consistent artifacts with cross-linking
- Agent-to-skills mapping via frontmatter `skills:` field
- Optional observability via TRACE Envelope

## Directory Structure

```text
.
├── README.md                               # This file
├── LICENSE                                 # MIT license
└── .claude/                                # Claude Code integration root
    ├── CLAUDE.md                           # Project-level config (slim)
    ├── agents/                             # Agent definitions
    │   ├── sdd-architect.md                # Spec/proposal design
    │   ├── sdd-feasibility-analyst.md      # Option comparison & decisions
    │   ├── sdd-strategic-planner.md        # Task decomposition & slicing
    │   ├── sdd-implementer.md              # Code implementation
    │   ├── sdd-code-reviewer.md            # Code review (read-only)
    │   ├── sdd-test-runner.md              # Test execution & evidence
    │   └── sdd-doc-sync.md                 # Documentation sync
    ├── skills/                             # Skill definitions
    │   ├── sdd-common/SKILL.md             # Common skills
    │   └── sdd-*/SKILL.md                  # Role-specific skills
    ├── rules/                              # Auto-loaded rules
    │   └── dual-sdd/
    │       ├── docs.md                     # Documentation rules
    │       ├── testing.md                  # Testing rules
    │       ├── style.md                    # Code style rules
    │       ├── security.md                 # Security rules
    │       └── docs/                       # Path-scoped rules
    │           ├── prd.md                  # For spec.md/proposal.md
    │           └── feasibility.md          # For decisions.md
    └── moyu/                               # Artifact storage
        ├── specs/                          # SpecKit artifacts
        ├── openspec/                       # OpenSpec system
        │   ├── changes/                    # Change proposals
        │   └── specs/                      # Truth specs
        ├── templates/                      # Canonical templates
        ├── docs/                           # Development docs
        │   ├── architecture.md             # Pack architecture
        │   └── doc-types.md                # Document type definitions
        ├── trace/                          # Trace logs
        └── .specify/                       # Specify scaffolding

```

## Installation

### Option 1: Global Installation (Recommended)

```bash
# Clone this repository
git clone https://github.com/xianxianxianyu/claude-code-skills.git
cd claude-code-skills/dual-sdd

# Copy to global .claude directory
# Windows
xcopy /E /I .claude "%USERPROFILE%\.claude"

# macOS/Linux
cp -r .claude ~/.claude/
```

**Note**: When installing multiple packs, rules are namespaced under `rules/<pack>/` to avoid conflicts.

### Option 2: Project-Specific Installation

```bash
cd /path/to/your/project

git clone https://github.com/xianxianxianyu/claude-code-skills.git temp-skills
cp -r temp-skills/dual-sdd/.claude .
rm -rf temp-skills
```

### Verify Installation

Check that these agents are available in Claude Code:
- `sdd-architect`
- `sdd-feasibility-analyst`
- `sdd-strategic-planner`
- `sdd-implementer`
- `sdd-code-reviewer`
- `sdd-test-runner`
- `sdd-doc-sync`

## Usage

### 1. Create a Work Item (WI)

Format: `WI-YYYYMMDD-###-slug`
Example: `WI-20260121-001-user-auth`

### 2. Choose MODE

| MODE     | Truth Source                     | Use Case                          |
| -------- | -------------------------------- | --------------------------------- |
| SpecKit  | `.claude/moyu/specs/<WI>/`       | New modules, linear governance    |
| OpenSpec | `.claude/moyu/openspec/specs/**` | Incremental changes, multi-module |

### 3. Execute Pipeline

```
Phase A: Specification (serial + human gate)
  1. sdd-architect → spec.md / proposal.md
  2. sdd-feasibility-analyst → decisions.md
  3. Human confirmation
  4. sdd-strategic-planner → tasks.md + slices/

Phase B: Implementation (parallelizable)
  5. sdd-implementer (by slice)
  6. sdd-code-reviewer
  7. sdd-test-runner → evidence/
  8. Fix loop if needed

Phase C: Documentation (required)
  9. sdd-doc-sync → .claude/moyu/docs/
  10. Final acceptance
```

### 4. Close-out

- **SpecKit**: Ensure `spec.md/plan.md/tasks.md` match implementation
- **OpenSpec**: Merge final behavior into `.claude/moyu/openspec/specs/**`
- Update `.claude/moyu/docs/**` as needed

## Agent-Skill Mapping

Each agent declares its skills via frontmatter:

```yaml
---
name: sdd-architect
skills:
  - sdd-common      # Common skills
  - sdd-architect   # Role-specific skills
---
```

| Agent                   | Skills                      |
| ----------------------- | --------------------------- |
| sdd-architect           | sdd-common, sdd-architect   |
| sdd-feasibility-analyst | sdd-common, sdd-feasibility |
| sdd-strategic-planner   | sdd-common, sdd-planner     |
| sdd-implementer         | sdd-common, sdd-implementer |
| sdd-code-reviewer       | sdd-common, sdd-reviewer    |
| sdd-test-runner         | sdd-common, sdd-tester      |
| sdd-doc-sync            | sdd-common, sdd-docsync     |

## Contributing

Issues and PRs are welcome.

- Keep changes small and reviewable
- All SDD artifacts must live under `.claude/moyu/`
- Update `CLAUDE.md` and related files when changing paths

## License

MIT. See `LICENSE`.
