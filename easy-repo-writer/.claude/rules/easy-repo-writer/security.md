# Security Rules for ERW Pack

## Guardrails
- Never run destructive commands without confirmation
- Never write secrets into documentation
- Flag suspicious secret files

## Publishing Safety
- Default publish=patch (no repo root modification)
- publish=sync requires explicit user request
- Always list modified files before sync
