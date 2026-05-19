# /release-notes — Generate release notes from commits

## Inputs
Either:
- A version range: `v1.2.0..HEAD` or `v1.2.0..v1.3.0`
- A target version tag to cut (I'll infer the previous tag)
- Nothing — in which case ask me which range to cover before continuing.

## Steps

### 1. Gather commits
- Run `git log <range> --no-merges --pretty=format:"%h %s"`.
- If the project uses Conventional Commits, group by type:
  **Features** (feat), **Fixes** (fix), **Performance** (perf),
  **Refactors** (refactor), **Docs** (docs), **Other** (chore, build, ci, test).
- If commits are not conventional, group by file area instead
  (use the directories most affected).

### 2. Filter noise
- Drop pure formatting, typo fixes, and dependency bumps **unless**
  a dependency bump is security-relevant or breaks API.
- Squash duplicate or revert-pair commits into a single line or omit.

### 3. Write the notes
Produce this structure in a fenced markdown block:

```
## <version> — <YYYY-MM-DD>

### Highlights
- 1–3 bullets. The reason a user would care about this release.

### Features
- <short imperative description> (#PR or commit-hash)

### Fixes
- <what was broken, now fixed> (#PR or commit-hash)

### Breaking changes
- <what changed, who is affected, how to migrate>

### Internal
- <refactors, infra, tooling changes worth noting>
```

### 4. Detect breaking changes
- Anything with `!` in the commit type (`feat!:`, `fix!:`) or a
  `BREAKING CHANGE:` footer goes under **Breaking changes** with a
  one-line migration note.
- If you find a breaking change with no migration note, ask me before
  publishing.

## Constraints
- One sentence per bullet. No marketing language.
- Link PR numbers only if they appear in the commit messages.
- If the range produces nothing user-visible, say so — don't pad.
- Never invent version numbers or dates. Ask if unclear.
