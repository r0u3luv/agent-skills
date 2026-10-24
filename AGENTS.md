# AGENTS.md

## Engineering Style

Prefer small, reviewable changes that follow the local codebase style.

Before editing, inspect the surrounding files and existing patterns. Use the project's existing framework, helper APIs, and test conventions unless there is a clear reason to introduce something new.

When reporting work, lead with behavior changed, files touched, and verification performed.

## Testing

Scale testing to risk.

For narrow changes, run the closest focused test. For shared behavior, API contracts, data migrations, or user-facing flows, add or run broader coverage. If tests cannot be run, state the reason and the residual risk.
