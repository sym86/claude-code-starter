# Coding Conventions

## General
- Optimize for readability over cleverness.
- Functions do one thing. If a function needs an "and" in its name, split it.
- Comment *why*, not *what*. The code shows what; comments explain rationale.

## Naming
- Variables and functions: descriptive, no single-letter names except
  loop indices and well-known math conventions.
- Booleans: `is`, `has`, `should`, `can` prefixes.
- Constants: `SCREAMING_SNAKE_CASE`.

## Error Handling
- Never swallow errors silently. Log, re-throw, or handle explicitly.
- User-facing errors: actionable message, no stack traces.
- Internal errors: include enough context to debug without re-running.

## Imports
- Standard library first, third-party second, local last. Blank line
  between groups.
- No wildcard imports.

## Comments & Docs
- Public functions/classes get a docstring describing inputs, outputs,
  and side effects.
- TODOs must include an issue link or a name and date.
