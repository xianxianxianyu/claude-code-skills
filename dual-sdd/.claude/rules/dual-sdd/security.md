# Security Rules for SDD Pack

## Blocker-Level Issues
- SQL injection, XSS, Command injection
- Data loss risks, Core constraint violations

## Sensitive Data
- Never commit secrets or credentials
- Exclude .env and credential files

## Audit Trail
- All phase transitions logged to `.claude/moyu/trace/runs.jsonl`
