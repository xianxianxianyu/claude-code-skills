# Moyu Dual SDD Skills (SpecKit / OpenSpec)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

Read this in Chinese: [`README.zh-CN.md`](README.zh-CN.md)

This repository is a Spec-Driven Development (SDD) scaffold with a dual-mode workflow:

- SpecKit: greenfield work, new modules, linear governance
- OpenSpec: incremental changes, multi-module work, auditability

The core design goal is simple: keep every SDD artifact under `.claude/moyu/` so your repo root stays clean and reviews stay deterministic.

## Features

- Dual SDD modes with a single-source-of-truth rule per Work Item (WI)
- Deterministic artifact paths (fast to locate context/spec/tasks/evidence)
- "Entry shim" subagents under `.claude/agents/` for Claude Code discovery, while keeping canonical agent prompts under `.claude/moyu/agents/`
- Shared templates under `.claude/moyu/templates/` for consistent artifacts
- Skills library + agent-to-skills mapping via `.claude/moyu/skills/manifest.yaml`
- Optional observability via TRACE Envelope (see `.claude/moyu/skills/common/07-TraceEnvelope.md`)

## Layout (tree)

```text
.
├── CLAUDE.md                               # Plan Agent manual + mode/path rules (single source of truth for workflow)
├── README.md                               # This file
├── LICENSE                                 # MIT license
└── .claude/                                # Claude Code integration root
    ├── agents/                             # Entry layer: shims so Claude Code can discover subagents
    │   ├── sdd-architect.md                # shim -> .claude/moyu/agents/sdd-architect.md
    │   ├── sdd-feasibility-analyst.md      # shim -> .claude/moyu/agents/sdd-feasibility-analyst.md
    │   ├── sdd-strategic-planner.md        # shim -> .claude/moyu/agents/sdd-strategic-planner.md
    │   ├── sdd-implementer.md              # shim -> .claude/moyu/agents/sdd-implementer.md
    │   ├── sdd-code-reviewer.md            # shim -> .claude/moyu/agents/sdd-code-reviewer.md
    │   ├── sdd-test-runner.md              # shim -> .claude/moyu/agents/sdd-test-runner.md
    │   └── sdd-doc-sync.md                 # shim -> .claude/moyu/agents/sdd-doc-sync.md
    └── moyu/                               # Canonical namespace: all SDD artifacts + prompts live here
        ├── agents/                         # Real subagent prompts (authoritative source)
        ├── templates/                      # Canonical templates (common/speckit/openspec)
        ├── skills/                         # Skills library (includes manifest.yaml mapping agents -> skills)
        ├── specs/                          # SpecKit artifacts: .claude/moyu/specs/<WI>/...
        ├── openspec/                       # OpenSpec system
        │   ├── changes/                    # Change proposals: .claude/moyu/openspec/changes/<WI>/...
        │   ├── specs/                      # Truth specs: .claude/moyu/openspec/specs/** (must reflect final behavior)
        │   └── archive/                    # Archived / closed-out changes (optional)
        ├── docs/                           # Development docs: .claude/moyu/docs/** (kept in sync)
        ├── .specify/                       # Specify scaffolding (memory + templates)
        └── trace/                          # Trace logs (optional): runs.jsonl + protocol docs
```

## Usage Guide

1) Read `CLAUDE.md` first (this defines MODE routing, ARTIFACT_ROOT rules, and gates).

2) Create a Work Item (WI):
   - Format: `WI-YYYYMMDD-###-slug`
   - Example: `WI-20260121-001-user-auth`

3) Pick exactly one MODE per WI:
   - SpecKit: `.claude/moyu/specs/<WI>/` is the truth source for that WI
   - OpenSpec: `.claude/moyu/openspec/specs/**` is truth, `.claude/moyu/openspec/changes/<WI>/` is the isolated change folder

4) Use subagents (via `.claude/agents/*.md` shims):
   - The shim points you to the canonical prompt under `.claude/moyu/agents/*.md`.
   - Follow the role-specific skills under `.claude/moyu/skills/**`.

5) Copy templates and write artifacts:
   - Templates live at `.claude/moyu/templates/**`.
   - Evidence should be written under `ARTIFACT_ROOT/evidence/` (commands + result summaries).

6) Close-out:
   - SpecKit: ensure `spec.md/plan.md/tasks.md` match reality.
   - OpenSpec: ensure final behavior is merged into `.claude/moyu/openspec/specs/**` (truth), not left only in changes.
   - Update `.claude/moyu/docs/**` as needed.

## Contributing

Issues and PRs are welcome.

- Keep changes small and reviewable.
- Do not introduce root-level `specs/`, `openspec/`, `docs/`, or `.specify/` directories; all SDD artifacts live under `.claude/moyu/`.
- If you change any paths, update `CLAUDE.md`, shims in `.claude/agents/`, and any referenced skills/templates/docs to stay consistent.

## License

MIT. See `LICENSE`.
