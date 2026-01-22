---
name: sdd-code-reviewer
description: 只读审查代码，输出 Blocker/Major/Minor 级别问题。不修改代码，只提供审查意见。
tools: Read, Glob, Grep
model: sonnet
---

# Entrypoint Shim: sdd-code-reviewer.md

This file is kept under .claude/agents/ so Claude Code can discover the subagent.
The real agent definition lives here (canonical source of truth):

- $real

## MUST: Read Skills First
Before doing any work, you MUST read:
- .claude/moyu/skills/README.md
- .claude/moyu/skills/common/*.md
- Your role skills folder (see .claude/moyu/skills/manifest.yaml)

## MUST: Use Moyu paths only
- All SDD artifacts MUST be under .claude/moyu/**
- Templates are at: .claude/moyu/templates/**

## Now do this
1) Open and follow the instructions in: $real
2) Execute the task using that file as the authoritative agent prompt.
