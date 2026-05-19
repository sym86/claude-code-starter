# /onboard — Get the lay of the land in an unfamiliar repo

## When to use
First time opening this repo (or returning after months away) and you
need a fast, accurate mental model before touching anything.

## Steps

### 1. What is this?
- Read `README.md` (top 100 lines).
- Read `package.json` / `pyproject.toml` / `go.mod` / `Cargo.toml` —
  whichever exists. Note: name, description, main entry, runtime version,
  declared scripts/commands.
- Output a 2-sentence summary: **what this project does** and **what it
  doesn't do** (scope boundaries).

### 2. Stack & tooling
List, with file:line evidence:
- Language(s) and version
- Framework(s) and major libraries
- Build / run / test commands (from `scripts` block or Makefile)
- Linter / formatter / type-checker config files present
- CI workflows present (`.github/workflows/*`)

### 3. Layout
- Print the top-level directory tree (depth 2). For each non-obvious
  folder, give a one-line purpose inferred from contents.
- Identify the **entry point** (main file) and the **public API surface**
  (exported modules, route definitions, CLI commands).

### 4. How code flows
Pick the most important user-facing capability and trace it end-to-end
in ≤ 5 hops: entry → router/handler → service → data layer → response.
Cite file:line at each hop. If you can't find a clear flow, say so.

### 5. Conventions in use
Infer from existing code:
- File/folder naming (kebab-case / snake_case / PascalCase)
- Test framework and where tests live
- Error handling style (throw, Result type, error returns)
- Logging style (console, structured logger, none)
- Commit message style (look at `git log --oneline -20`)

### 6. Risk surface
- Anything in `/migrations`, `/generated`, or `/vendor` to avoid touching.
- Files with `TODO`, `FIXME`, `HACK` markers (count + top 3 by recency).
- Environment variables required to run (from `.env.example` or code grep).

### 7. Output
End with three short lists:
- **To run this:** the exact commands, in order.
- **To test this:** the exact commands.
- **Open questions:** anything you couldn't answer from the code alone.

## Constraints
- Read; don't run code without asking.
- Cite file:line for every claim. No vague "appears to use X".
- If the repo is huge (>1000 files), narrow to the most-edited 10%
  (use `git log --pretty=format: --name-only | sort | uniq -c | sort -rn | head -50`).
- Stop and ask before grepping the whole repo for secrets or PII.
