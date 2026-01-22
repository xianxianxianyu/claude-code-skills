# Trace Observability (Plan -> Subagent -> Skills)

This folder stores append-only trace logs.

## Protocol: TRACE Envelope (required in every agent response)
Each response MUST start with a machine-parseable block:

[TRACE]
run_id: <unique>
parent_id: <optional>
agent: <plan_agent|sdd-...>
subagent: <if any>
mode: <speckit|openspec>
work_item: <WI-...>
skills:
  - <SkillID> <SkillName>
artifacts_written:
  - <path>
gates:
  - <GateName>: PASS|FAIL|N/A
[/TRACE]

## Log file
- runs.jsonl: one JSON event per line (append-only)

