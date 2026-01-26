# Code Style Rules for SDD Pack

## General Principles
- Small incremental changes preferred
- Avoid large-scale refactoring
- Keep code compilable at all times

## Boundary Enforcement
- Only modify files within allowed paths
- Out-of-bounds = immediate stop + blocker report

## Naming Conventions
- WI ID: `WI-YYYYMMDD-###-slug`
- Slice files: `slices/<slice_name>.md`
- Evidence files: `evidence/<action_name>.md`
