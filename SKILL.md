---
name: clean
description: Keep any project clean, whatever the language or stack. Use on every task that changes files, writes comments, runs throwaway experiments, adds temporary stand-ins, or prepares a commit.
---

# Clean

**Core rule:** the final diff contains only what the task needs. Anything else is either temporary (kept out of the repo and removed) or out of scope (left alone).

## 1. Scope
Clean only your own changes, meaning the diff against the base branch. Don't fix pre-existing clutter unless asked; mention serious issues in your summary instead.

## 2. Comments
Test for every comment: *could a competent reader get this from the code itself?* If yes, improve names or structure and drop the comment. Keep only:
- **why** something non-obvious is done (constraint, workaround, business rule);
- concise docs for public interfaces.

Remove: restatements of the code, step-by-step narration, edit history ("previously", "now uses", "no longer", "added/fixed"; history belongs in commits), tool or decompiler artifacts, disabled code, notes addressed to the reader.

Never remove: tool directives (linter, compiler, type-checker pragmas), license headers, generated-code markers, TODO/FIXME with a reason, issue or spec references, notes explaining test intent.

When a change only touches comments, confirm the code itself is unchanged.

## 3. Code
No leftover debug output, unused symbols, dead branches, or test-only switches. Don't add defensive checks, error handling, or type escapes beyond what the surrounding code does. Match the file's existing style.

## 4. Files
- Scratch work (experiments, one-off scripts, logs, dumps, samples) goes only into `.clean/` at the project root. Ignore it locally (for git: add `.clean/` to `.git/info/exclude`), never via the shared ignore file.
- No copies or variants of real files; edit the original, version control is the backup.
- Prefer editing existing files. Create new ones only when the structure calls for it; no unrequested notes or docs. Delete files you created that ended up unused.

## 5. Temporary stand-ins
Anything added only so you can run or test something yourself (fake data, mocks, substitute services, bypassed checks, edited config, data written to real storage) must be gone before you finish.
- Keep it in `.clean/` when possible; otherwise mark the line with `TEMP-STUB`.
- Afterwards: restore code and config, delete data you created, stop processes you started.
- Never fake success. If you couldn't test against the real dependency, say so. If a stand-in must stay, tell the user what, where, and what replaces it.
- Test doubles in the project's real test suite are not temporary.

## 6. Never enters the repo
- Secrets and real credentials: read them from the environment; add only empty placeholders to the project's example config. If you spot one already committed, tell the user to rotate it.
- Real personal or production data.
- Generated, build, dependency, environment, OS, or editor files. If ignore rules miss something, suggest the addition instead of committing it.
- Dependencies you tried but don't use, unrelated lock-file churn, a second package manager's files.

## 7. Before finishing
1. Review status and the full diff: every changed file and line is intentional.
2. Stage files explicitly by path, never everything at once.
3. Search your diff for `TEMP-STUB` and edit-history wording; both must be gone.
4. Empty `.clean/` and confirm nothing from it is staged.
5. Report: files changed, anything untested against real dependencies, stand-ins left on purpose, suggested ignore rules or exposed secrets.
