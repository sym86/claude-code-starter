# /commit-msg — Generate a commit message from staged changes

## Steps
1. Run `git diff --cached` to see staged changes. If nothing is staged,
   stop and tell me.
2. Identify the dominant change type: feat, fix, refactor, docs, test,
   chore, perf, build, ci.
3. Identify the scope (the directory or module most affected).
4. Write a Conventional Commits message:
   `<type>(<scope>): <imperative summary, <=72 chars>`
5. If the diff is non-trivial (>20 lines or touches >2 files), add a
   body: blank line, then 1–3 bullets explaining *why*, not *what*.
6. Output the message in a fenced block. Do not run `git commit`
   yourself — I'll do that.

## Constraints
- Imperative mood ("add", not "added" or "adds").
- No trailing period on the subject line.
- No emojis unless I've used them in recent commits.
- Never invent context that isn't in the diff.
