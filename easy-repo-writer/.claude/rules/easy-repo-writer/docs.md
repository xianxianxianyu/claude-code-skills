# Documentation Rules for ERW Pack

## Output Location
- Default: `.claude/moyu/docs/easy-repo-writer/runs/<RUN_ID>/`
- Never pollute repo root without explicit consent

## Three-Perspective Coverage (Mandatory)
1. Journey: Adopt -> Integrate -> Operate -> Extend -> Contribute
2. System: Context -> Component -> Code -> Runtime
3. Product: Problem -> Positioning -> Differentiators -> Adoption

## Document Structure
1. What / When (purpose)
2. Run it now (minimal example)
3. Mental model (analogy + diagram)
4. API / Config (reference)
5. Gotchas (pitfalls + solutions)
6. Deep dive (optional)

## Writing Constraints
- No vague statements - reference specific files/interfaces
- README first screen must include quickstart command
- Unverifiable commands marked as TODO
