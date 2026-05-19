# Project Instructions for Claude Code

> Keep this file lean. If a section grows past ~30 lines, move it to a file
> under `docs/` and replace it with a one-line pointer in the Routing Map.
## 0. Stack

**TypeScript + Node.js.** See `docs/conventions.md` for the full
language/style rules.

## 1. Memory System

- At the **start of every session**, read `.claude/memory.md` for active context.
- Do **not** read `.claude/archive.md` unless I explicitly ask about
historical decisions ("what did we decide about X last month?").
- At the **end of a meaningful session**, propose updates to `memory.md`.
Move anything older than ~2 weeks or no longer active into `archive.md`.

## 2. Preferences

- **Tone:** concise, direct, no filler. Skip apologies and preamble.
- **Format:** prose for explanations; code blocks for code; bullets only
when listing 3+ parallel items.
- **Length:** match the question. One-line questions get one-line answers.
- **Uncertainty:** say "I'm not sure" rather than guessing. Cite the file
and line when referencing code.

## 3. Rules (hard constraints)

- Always run the project's tests/linter before claiming a task is done.
- Never edit files in `/migrations`, `/generated`, or `/vendor` without
asking first.
- Never commit secrets, API keys, or `.env*` contents. If you see one,
flag it.
- Never force-push, rewrite shared history, or delete branches without
explicit confirmation.
- Prefer the smallest diff that solves the problem. No drive-by refactors.
- If a task is ambiguous, ask one clarifying question before starting.
- Before creating any new file, read `docs/file-conventions.md`.

## 4. Routing Map

Use this table to decide which reference doc to load based on the task.
Load **only what's needed** — don't preload everything.

| If the task involves... | Load this file |
| ------------------------------------ | ----------------------------- |
| Coding style, naming, structure | `docs/conventions.md` |
| Creating a new file or module | `docs/file-conventions.md` |
| Orienting in an unfamiliar repo | `.claude/commands/onboard.md` |
| Writing a commit message | `.claude/commands/commit-msg.md` |
| Drafting a PR description | `.claude/commands/pr-desc.md` |
| Adding tests for existing code | `.claude/commands/add-test.md` |
| Self-reviewing a diff before push | `.claude/commands/code-review.md`|
| Debugging an error or stack trace | `.claude/commands/debug-trace.md`|
| Planning a refactor before coding | `.claude/commands/refactor-plan.md`|
| Security-auditing a diff or file | `.claude/commands/security-review.md`|
| Cutting a release / generating notes | `.claude/commands/release-notes.md`|
| Recalling historical decisions | `.claude/archive.md` |

## 5. References (on-demand only)

- `docs/conventions.md` — TypeScript + Node coding style, naming, error handling
- `docs/file-conventions.md` — where new files go, headers, boilerplate
- `.claude/archive.md` — historical decisions, completed work log

## 6. Creating New Workstations / Skills

When I ask to add a new repeatable workflow:
- If it's an **ongoing area of work** (needs accumulated context, judgment
calls) → propose a new subfolder with its own `CLAUDE.md` and `memory.md`.
- If it's a **deterministic checklist** (same steps every time) → propose
a new file in `.claude/commands/` and add a row to the Routing Map.

Heuristic: *Is this a place I work, or a thing I do?* Place → workstation.
Thing → skill.
