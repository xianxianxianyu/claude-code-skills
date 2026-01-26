# Documentation Rules for SDD Pack

## Context File (context.md)
- Maximum 400 characters
- Must include: Phase, Status, Key Decisions, Touched Files, Next Steps
- Update at every phase transition

## Spec/Proposal Documentation
- GOAL: Single sentence, business-focused
- NON_GOALS: Explicit boundaries
- CONSTRAINTS: Technical and business limitations
- ACCEPTANCE: Minimum 2 testable criteria

## Evidence Documentation
- Location: `ARTIFACT_ROOT/evidence/`
- Required: Command, Result, Summary, Timestamp (ISO8601)

## Cross-Reference Requirements
- spec.md MUST link to decisions.md
- decisions.md MUST reference originating spec.md/proposal.md
- tasks.md MUST reference both spec and decisions
