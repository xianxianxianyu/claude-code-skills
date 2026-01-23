# Claude Code Skills Collection

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

[中文版](README.zh-CN.md)

A collection of Claude Code skill packs to supercharge your development workflow.

## What's Inside

| Skill Pack                                | Description                                                                   | Best For                                                            |
| ----------------------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| [**Dual SDD**](dual-sdd/)                 | Spec-Driven Development scaffold with dual-mode workflow (SpecKit / OpenSpec) | Teams needing structured spec → plan → implement → review workflows |
| [**Easy Repo Writer**](easy-repo-writer/) | Auto-generate comprehensive documentation for any repository                  | Quick documentation generation for existing projects                |

---

## Dual SDD

A complete Spec-Driven Development framework with:

- **SpecKit Mode**: For greenfield projects, new modules, linear governance
- **OpenSpec Mode**: For incremental changes, multi-module work, auditability
- **7 Specialized Agents**: Architect, Feasibility Analyst, Strategic Planner, Implementer, Code Reviewer, Test Runner, Doc Sync
- **9 Skill Sets**: Common utilities + role-specific skills
- **Gate System**: Enforced checkpoints between phases

**Quick Start:**
```bash
# Copy to your project
cp -r dual-sdd/.claude /path/to/your/project/
```

[Read more →](dual-sdd/README.md)

---

## Easy Repo Writer

Auto-generate documentation using a 3-agent pipeline:

- **erw-planner**: Scans repo, creates documentation plan
- **erw-writer**: Generates multi-perspective docs (journey, system views, positioning)
- **erw-publisher**: QA checks, creates publish package

**Quick Start:**
```bash
# In Claude Code
/easy-repo-writer
```

[Read more →](easy-repo-writer/README.md)

---

## Installation

### Option 1: Install Everything (Global)

```bash
git clone https://github.com/xianxianxianyu/claude-code-skills.git
cd claude-code-skills

# Windows
xcopy /E /I dual-sdd\.claude "%USERPROFILE%\.claude"
xcopy /E /I easy-repo-writer\.claude "%USERPROFILE%\.claude"

# macOS/Linux
cp -r dual-sdd/.claude ~/.claude/
cp -r easy-repo-writer/.claude ~/.claude/
```

### Option 2: Install Specific Pack

```bash
# Just Dual SDD
cp -r dual-sdd/.claude /path/to/your/project/

# Just Easy Repo Writer
cp -r easy-repo-writer/.claude /path/to/your/project/
```

### Option 3: Cherry-pick Components

Each pack is modular. You can copy individual agents or skills:

```bash
# Just the architect agent
cp dual-sdd/.claude/agents/sdd-architect.md /path/to/your/project/.claude/agents/

# Just the easy-repo-writer skill
cp -r easy-repo-writer/.claude/skills/easy-repo-writer /path/to/your/project/.claude/skills/
```

---

## Quick Comparison

| Feature      | Dual SDD                                     | Easy Repo Writer            |
| ------------ | -------------------------------------------- | --------------------------- |
| **Purpose**  | Structured development workflow              | Documentation generation    |
| **Agents**   | 7 (spec, plan, implement, review, test, doc) | 3 (plan, write, publish)    |
| **Workflow** | Multi-phase with gates                       | Single pipeline             |
| **Output**   | Specs, plans, tasks, code, tests, docs       | Documentation only          |
| **Best for** | New features, refactoring, team projects     | Existing repos needing docs |

---

## Directory Structure

```
claude-code-skills/
├── README.md                    # This file
├── README.zh-CN.md              # Chinese version
├── LICENSE                      # MIT
├── dual-sdd/                    # Dual SDD skill pack
│   ├── README.md
│   ├── README.zh-CN.md
│   └── .claude/
│       ├── agents/              # 7 SDD agents
│       ├── skills/              # 9 skill sets
│       └── moyu/                # Artifact storage
└── easy-repo-writer/            # Easy Repo Writer skill pack
    ├── README.md
    ├── README.zh-CN.md
    └── .claude/
        ├── agents/              # 3 ERW agents
        ├── skills/              # ERW skills
        └── moyu/                # Templates & output
```

---

## Contributing

Issues and PRs are welcome!

- Keep changes small and reviewable
- Each skill pack should be self-contained
- Update relevant READMEs when making changes

## License

MIT. See [LICENSE](LICENSE).
