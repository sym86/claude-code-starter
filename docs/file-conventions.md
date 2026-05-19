# File Conventions

> Read this before creating any new file.

## Where things go
- **Source code:** mirrors the public API structure. One primary export per file.
- **Tests:** parallel path to the source file, with the project's
  test suffix (e.g. `foo.test.ts`, `test_foo.py`, `foo_test.go`).
- **Docs:** under `docs/`. Markdown only. One topic per file.
- **Scripts:** under `scripts/`. Each script has a header comment
  explaining purpose and usage.
- **Generated files:** never edited by hand. If you need to change
  them, change the generator.

## Required file header
For source files in languages that support it, the first non-shebang
line should be a one-line comment describing the file's purpose.

## Before creating a new file, confirm
1. Does an existing file already cover this responsibility?
2. Is the location consistent with similar existing files?
3. Is the filename in the project's casing convention
   (kebab-case, snake_case, or PascalCase — match neighbors)?
4. Does it need a corresponding test file?

If you can't answer all four, ask me first.
