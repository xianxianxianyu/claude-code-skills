# Easy Repo Writer

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](../LICENSE)

Read this in Chinese: [`README.zh-CN.md`](README.zh-CN.md)

A Claude Code skill pack that automatically generates comprehensive, readable documentation for any repository using a 3-agent pipeline.

## Features

- **3-Agent Pipeline**: Planner → Writer → Publisher
- **Multi-perspective Documentation**: Journey axis + System views + Product positioning
- **Bilingual Support**: Generate docs in Chinese, English, or both
- **Safe Publishing**: Default patch mode - generates change packages without modifying repo
- **Customizable Depth**: Quick overview, standard docs, or deep analysis
- **Auto-loaded rules** in `.claude/rules/easy-repo-writer/` for consistent policies

## Directory Structure

```text
easy-repo-writer/
└── .claude/
    ├── CLAUDE.MD                            # Project-level config (slim)
    ├── agents/                              # Agent definitions
    │   ├── erw-planner.md                   # Scans repo, creates doc plan
    │   ├── erw-writer.md                    # Generates documentation
    │   └── erw-publisher.md                 # QA checks, creates publish package
    ├── skills/
    │   └── easy-repo-writer/
    │       ├── SKILL.md                     # Entry point skill
    │       └── skills/                      # Internal skills
    │           ├── 00-ERW-Protocol.md
    │           ├── planner/                 # Planning skills
    │           ├── writer/                  # Writing skills
    │           └── publisher/               # Publishing skills
    ├── rules/                               # Auto-loaded rules
    │   └── easy-repo-writer/
    │       ├── docs.md                      # Documentation rules
    │       ├── testing.md                   # QA rules
    │       ├── style.md                     # Style rules
    │       └── security.md                  # Security rules
    └── moyu/
        ├── templates/easy-repo-writer/      # Doc templates
        └── docs/easy-repo-writer/runs/      # Output directory
```

## Installation

Copy the `.claude` directory to your project root:

```bash
# From this repo
cp -r easy-repo-writer/.claude /path/to/your/project/
```

Or for global installation:

```bash
# Windows
xcopy /E /I easy-repo-writer\.claude "%USERPROFILE%\.claude"

# macOS/Linux
cp -r easy-repo-writer/.claude ~/.claude/
```

**Note**: When installing multiple packs, rules are namespaced under `rules/<pack>/` to avoid conflicts.

## Usage

In Claude Code, invoke the skill:

```bash
# Default: Chinese, standard depth, patch mode
/easy-repo-writer

# With options
/easy-repo-writer --lang=en --depth=deep --publish=preview
```

### Parameters

| Parameter | Options | Default | Description |
|-----------|---------|---------|-------------|
| `--lang` | `zh`, `en`, `bilingual` | `zh` | Output language |
| `--depth` | `quick`, `standard`, `deep` | `standard` | Documentation depth |
| `--stage` | `plan`, `write`, `publish`, `all` | `all` | Which stages to run |
| `--publish` | `preview`, `patch`, `sync` | `patch` | Publishing mode |

### Publishing Modes

- **preview**: Generate to `.claude/moyu/docs/` only, no publish package
- **patch**: Generate a publish package with change manifest (safe, recommended)
- **sync**: Directly modify repo root files (requires explicit user consent)

## Output

All outputs go to:

```
.claude/moyu/docs/easy-repo-writer/runs/<RUN_ID>/
├── 00-context/
│   └── repo-profile.md          # Repository analysis
├── 01-plan/
│   ├── doc-map.md               # Documentation structure
│   └── tasks.md                 # Writing tasks
├── 02-drafts/
│   ├── index.md                 # Navigation entry
│   └── *.md                     # Generated docs
└── 03-publish/
    ├── report.md                # QA report
    └── patch/                   # Files ready to publish
```

## Pipeline Overview

```
erw-planner          erw-writer           erw-publisher
    │                    │                     │
    ▼                    ▼                     ▼
Scan repo ──────► Generate docs ──────► QA + Package
    │                    │                     │
repo-profile.md     02-drafts/*.md        patch/
doc-map.md          index.md              report.md
tasks.md
```

## License

MIT. See [`LICENSE`](../LICENSE).
