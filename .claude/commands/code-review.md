# /code-review — Self-review a diff before push

## Steps
1. Run `git diff <base-branch>...HEAD` (default base: `main`).
2. Review the diff against this checklist, in order. For each item,
   output a one-line verdict: ✅ pass, ⚠️ concern, ❌ blocker.

   - **Correctness** — does the code do what the PR claims?
   - **Tests** — new behavior is covered; no tests were weakened.
   - **Security** — no secrets, no SQL/command injection vectors,
     no unsafe deserialization, no logging of PII.
   - **Performance** — no obvious N+1, no unbounded loops, no sync
     I/O in hot paths.
   - **Error handling** — failures are handled or propagated, not swallowed.
   - **Naming & clarity** — names match intent; no dead code; no TODOs
     left behind without an issue link.
   - **Scope** — no unrelated changes hitching a ride.
   - **Conventions** — matches `docs/conventions.md`.

3. End with a summary: "Ready to push" or a numbered list of fixes needed.

## Constraints
- Cite file:line for every concern.
- Don't restate what the code does — only what's wrong or risky.
- If unsure whether something is intentional, ask, don't assume.
