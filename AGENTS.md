# AGENTS.md

This repository stores reusable AI agent skills and instructions.

## Source of Truth

The `.apm/` directory is canonical. Tool-specific files under `adapters/` are derived from it.

## Editing Guidelines

- Keep skill instructions short and procedural.
- Put large examples, schemas, policies, and detailed documentation in `references/`.
- Prefer scripts for fragile or repeated operations.
- Avoid storing secrets, customer data, or private credentials.
- Do not edit generated adapter output unless the change is also reflected in `.apm/`.

## Validation

When changing a skill, test it against at least one realistic fixture in `tests/skill-fixtures/` or record why validation was not needed.

