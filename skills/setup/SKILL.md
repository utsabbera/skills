---
name: setup
description: Wire up skills for a new project. Run once per project after adding the skills submodule. Reads existing AGENTS.md, lets the user pick which skills to install, and symlinks them into .claude/skills/.
---

Wire up selected skills for this project.

## Process

### 1. Read AGENTS.md

Read `AGENTS.md` from the repo root. This file is pre-existing — do not create or modify it. Extract the issue tracker type and commands if present; skills will fall back to `gh` if not found.

If `.skills/` submodule is missing, tell the user to run `git submodule add <url> .skills` first and stop.

### 2. Show available skills

List all skills in `.skills/skills/` with a one-line description of each. Check `.claude/skills/` for already-installed ones and mark them.

```
Available skills (.skills/skills/):
  [ ] ideate    — stress-test a plan through Socratic dialogue
  [x] tdd       — implement a feature test-first (already installed)
  [ ] prd       — write a PRD to docs/prd/
  [ ] breakdown — break a PRD into issues
  ...
```

### 3. Ask which to install

Ask the user which skills to add. Accept a list (e.g. "ideate, prd, breakdown") or "all". Existing installs are skipped unless the user says to reinstall.

### 4. Copy selected skills

```bash
mkdir -p .claude/skills
cp -r .skills/skills/<name> .claude/skills/<name>
```

Copy, not symlink — so each skill can be modified freely for this project without touching the submodule source.

Report each skill copied. If a skill already exists in `.claude/skills/`, skip it unless the user passed `--update <name>` or `--update all`, in which case overwrite with the latest from the submodule.
