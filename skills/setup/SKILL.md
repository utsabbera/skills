---
name: setup
description: Copy selected skills into .claude/skills/ for this project. Run once per project, pointing at a local clone of the skills repo. Reads existing AGENTS.md and lets the user pick which skills to install.
---

Copy selected skills into this project.

## Process

### 1. Find the skills source

If `$ARGUMENTS` contains a path, use it as the skills repo location. Otherwise ask: "Where is your local clone of the skills repo?"

Read `AGENTS.md` from the current project root — pre-existing, do not modify it. Extract issue tracker config if present; skills fall back to `gh` if absent.

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
cp -r <skills-repo>/skills/<name> .claude/skills/<name>
```

Copy, not symlink — each skill is now owned by this project and can be modified freely.

Skip skills that already exist in `.claude/skills/` unless the user passed `--update <name>` or `--update all`, in which case overwrite from the source repo.
