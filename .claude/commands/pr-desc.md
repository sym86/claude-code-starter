# /pr-desc — Draft a pull request description

## Steps
1. Determine the base branch (default: `main`). Run
   `git log --oneline <base>..HEAD` and `git diff <base>...HEAD --stat`.
2. Read up to 5 most-changed files to understand intent.
3. Produce a PR description with these sections:

   **Summary** — 2–3 sentences: what this PR does and why.
   **Changes** — bulleted list of concrete changes, grouped by area.
   **Testing** — how it was verified (commands run, manual checks).
   **Risk / Rollback** — what could break and how to revert.
   **Checklist** — tests pass, docs updated, no secrets, no TODOs left.

4. Output the description in a fenced markdown block.

## Constraints
- No marketing language ("massively improves", "blazing fast").
- Link to issues only if their numbers appear in commit messages.
- If you can't tell *why* from the diff alone, ask me before guessing.
