# claude-code-starter

A lean, opinionated starter pack for using **Claude Code** effectively on any
project. Inspired by Jeff Su's "Top 5 Claude Cowork Tips" — translated from
prompt-style workflows into a file-based structure Claude Code can actually
load on demand.

## Why this exists

LLM coding assistants get worse, not better, when you stuff their context with
everything. This repo encodes five practices that keep Claude Code sharp:

1. **Markdown Translator** — instructions live in markdown files, not in your head or chat history.
2. **300-Line Rule** — `CLAUDE.md` stays under ~300 lines; the rest is loaded on demand via the Routing Map.
3. **Memory Diet** — `memory.md` is active context only; everything stale moves to `archive.md`.
4. **Project Transplant** — drop this structure into any repo and it works.
5. **Skill Check** — repeatable workflows become slash commands in `.claude/commands/`.

## File tree

```
.
├── CLAUDE.md                          # Project entry point. Lean. Routes to everything else.
├── .claude/
│   ├── memory.md                      # Active context. Loaded every session.
│   ├── archive.md                     # Historical decisions. Loaded only on request.
│   └── commands/                      # Slash commands (deterministic workflows)
│       ├── commit-msg.md              # /commit-msg     — Conventional Commit from staged diff
│       ├── pr-desc.md                 # /pr-desc        — PR description from branch diff
│       ├── add-test.md                # /add-test       — Tests for a function/module
│       ├── code-review.md             # /code-review    — Self-review a diff before push
│       ├── debug-trace.md             # /debug-trace    — Diagnose an error or stack trace
│       ├── refactor-plan.md           # /refactor-plan  — Plan a refactor before coding
│       ├── security-review.md         # /security-review — Audit a diff for security issues
│       ├── release-notes.md           # /release-notes  — Generate release notes from commits
│       └── onboard.md                 # /onboard        — Get the lay of the land in a repo
└── docs/
    ├── conventions.md                 # Coding style, naming, error handling
    └── file-conventions.md            # Where new files go, headers, naming
```

## Use it in a new project

```bash
# 1. Use as a template (click "Use this template" on GitHub) OR clone and copy:
git clone https://github.com/sym86/claude-code-starter.git
cp -r claude-code-starter/{CLAUDE.md,.claude,docs} your-project/
cd your-project

# 2. Edit CLAUDE.md section 0 ("Stack") to match your language.
# 3. Edit docs/conventions.md to match your project's style.
# 4. Open Claude Code in your-project. It will pick up CLAUDE.md automatically.
```

## Slash commands at a glance

| Command            | When to use it                                          |
| ------------------ | ------------------------------------------------------- |
| `/commit-msg`      | You've staged changes and want a Conventional Commit.   |
| `/pr-desc`         | You're opening a PR and want a clean description.       |
| `/add-test`        | You want tests for an existing function or module.      |
| `/code-review`     | You want a self-review checklist before pushing.        |
| `/debug-trace`     | You have an error or stack trace to diagnose.           |
| `/refactor-plan`   | You're about to refactor and want a plan first.         |
| `/security-review` | You want a security audit of a diff or file.            |
| `/release-notes`   | You're cutting a release and need notes from commits.   |
| `/onboard`         | You just opened an unfamiliar repo. Orient yourself.    |

## Customizing

- **Different stack?** Replace section 0 of `CLAUDE.md` and rewrite
  `docs/conventions.md` for your language. Everything else is stack-agnostic.
- **New repeatable workflow?** Add a file under `.claude/commands/` and a row
  in the Routing Map in `CLAUDE.md`.
- **New ongoing area of work?** Create a subfolder with its own
  `CLAUDE.md` and `memory.md` (see CLAUDE.md section 6).

## License

MIT — see [LICENSE](./LICENSE). Fork, modify, and use freely.
