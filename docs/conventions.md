# Coding Conventions — TypeScript + Node.js

> Tailored for TypeScript on Node. If a section conflicts with project
> ESLint/Prettier config, the project config wins.

## General
- Optimize for readability over cleverness. A type that "looks ugly"
  but documents intent beats a clever one-liner.
- Functions do one thing. If a function name needs an "and", split it.
- Prefer pure functions where reasonable. Push side effects to the edges.
- Comment *why*, not *what*. The code shows what; comments explain rationale,
  invariants, and links to issues/specs.

## TypeScript
- `strict: true` in `tsconfig.json`. No exceptions.
- **No `any`.** Use `unknown` and narrow, or define the type. If you
  truly need an escape hatch, use `// eslint-disable-next-line` with a
  comment explaining why.
- Prefer `type` aliases for unions and function signatures; use
  `interface` for object shapes that may be extended.
- Use `readonly` arrays and properties by default. Mutability is opt-in.
- Use discriminated unions (`{ kind: "ok"; value: T } | { kind: "err"; error: E }`)
  over throwing for expected failure cases. Reserve `throw` for bugs
  and truly exceptional conditions.
- Don't widen types unnecessarily: use `as const` for literal tuples
  and config objects.
- No non-null assertions (`!`) in production code. Narrow with a guard
  or assert with a clear error.

## Async
- `async`/`await` everywhere. Never mix `.then()` chains with `await`.
- Always `await` Promises or return them — no fire-and-forget. If
  intentional, wrap in `void someAsyncFn()` and add a comment.
- Use `Promise.all` for parallel work; `Promise.allSettled` when you
  need every result regardless of failure.
- Add timeouts to every outbound network call (`AbortSignal.timeout(ms)`
  or library equivalent).

## Error Handling
- Never swallow errors. `catch { }` is banned — log, re-throw, or
  convert to a typed error.
- Define a small `AppError` (or domain-specific) class hierarchy.
  Wrap external errors at the boundary with `cause`.
- User-facing errors: actionable message, no stack traces, no
  internal IDs unless the user can act on them.
- Log errors with structured context (use `pino` or similar):
  `logger.error({ err, userId, requestId }, "checkout failed")`.

## Naming
- Variables and functions: `camelCase`, descriptive. No single-letter
  names except loop indices and standard math conventions.
- Types, interfaces, classes, enums: `PascalCase`. No `I` prefix on
  interfaces.
- Constants (module-level, truly invariant): `SCREAMING_SNAKE_CASE`.
- Booleans: `is`, `has`, `should`, `can` prefixes (`isReady`, `hasPaid`).
- Async functions: don't suffix with `Async` unless there's a sync
  sibling with the same name.
- Files: `kebab-case.ts` for modules, `PascalCase.tsx` only for
  React components.

## Imports
- Order: (1) Node built-ins (`node:fs`, `node:path`), (2) third-party,
  (3) local absolute (`@/...`), (4) local relative. Blank line between
  groups.
- Use the `node:` prefix for built-ins always.
- No default exports for modules with multiple symbols. Default exports
  are reserved for React components and config files.
- No wildcard imports (`import * as ...`) except for namespaces that
  are designed for it (e.g. `zod`).

## Modules & Structure
- One primary export per file. Helpers live alongside the thing they help.
- Public API of a directory goes in its `index.ts` — nothing else
  imports through deep paths.
- No circular imports. If you hit one, the abstraction is wrong.

## Environment & Config
- Never read `process.env` outside a single `config.ts` module.
- Validate config at startup with `zod` (or equivalent). Fail loud
  on missing/invalid env vars — don't fall back silently.
- Secrets only via env vars or a secret manager. Never check secrets
  into git, never log them, never put them in URLs.

## Testing
- Test runner: **Vitest** preferred (or Jest if the project already
  uses it). Match what's there.
- Co-locate tests: `foo.ts` ↔ `foo.test.ts` in the same directory.
- One assertion concept per test. Descriptive test names:
  `it("returns 404 when user is not found")`.
- No snapshot tests unless the project already uses them.
- Mock at the boundary (HTTP, DB, clock), not internal modules.
- Use `vi.useFakeTimers()` / `jest.useFakeTimers()` for any code that
  touches `Date.now()` or `setTimeout`.

## Lint & Format
- ESLint with `@typescript-eslint` recommended + `strict` rules.
- Prettier for formatting. Don't argue with it in code review.
- Pre-commit hook (lefthook/husky) runs lint + format on staged files.
- CI fails on any lint error. Warnings tracked but not blocking.

## Comments & Docs
- Public functions, classes, and exported types get a TSDoc comment
  describing inputs, outputs, side effects, and thrown errors.
- TODOs must include an issue link or a name and date:
  `// TODO(alice, 2026-06): batch these requests, see #423`.
- No commented-out code in commits. Delete it; git remembers.
