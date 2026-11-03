# clean

`clean` is an agent skill that keeps any project clean, regardless of language or stack. It enforces comment discipline, puts scratch work in a locally ignored `.clean/` folder, removes temporary stubs, and keeps secrets, generated artifacts, and unused dependencies out of the repository. Before finishing, it checks that the diff contains only what the task needs.

## Install

Clone this repository so the folder is named `clean`.

Claude Code, for your user:

```bash
git clone https://github.com/Xhiveee/clean.git ~/.claude/skills/clean
```

Claude Code, for one project:

```bash
git clone https://github.com/Xhiveee/clean.git .claude/skills/clean
```

Cursor:

```bash
git clone https://github.com/Xhiveee/clean.git .cursor/skills/clean
```
