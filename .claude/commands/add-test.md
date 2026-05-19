# /add-test — Add tests for a function or module

## Inputs
I'll point you at a file, function, or class. If I don't, ask which one.

## Steps
1. Detect the project's test framework from existing tests
   (e.g. Jest, Vitest, pytest, Go test, RSpec). Match the style exactly.
2. Locate or create the parallel test file using the project's
   convention (see `docs/file-conventions.md`).
3. Cover, in this order:
   - The happy path (1 test)
   - Each documented edge case (1 test each)
   - Error/failure modes (invalid input, thrown errors, rejections)
   - Boundary values (empty, null/undefined, max size) where relevant
4. Use existing test helpers and fixtures — do not invent new ones
   unless none exist.
5. Run the new tests. Report pass/fail. Do not modify source code to
   make tests pass without asking.

## Constraints
- One assertion concept per test. Descriptive test names.
- No snapshot tests unless the project already uses them.
- Never disable, skip, or weaken existing tests to get green.
