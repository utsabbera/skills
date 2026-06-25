---
name: setup
description: Initialize AGENTS.md and wire up skills for a new project. Run once per project after adding the skills submodule. Configures issue tracker, test command, and commit conventions.
---

Initialize this project for use with the skills workflow.

## Process

### 1. Check existing state

- If `AGENTS.md` already exists, read it and ask whether to update or skip.
- Check if `.skills/` submodule is present; if not, note that the user should run `git submodule add <url> .skills` first.

### 2. Detect what you can

Before asking, infer from the repo:
- **Issue tracker**: check for `.github/` (→ GitHub), `jira.config.*` or `atlassian` in deps (→ Jira), `linear` references (→ Linear)
- **Test command**: check `package.json` scripts, `Makefile`, `pyproject.toml`, `Justfile`
- **Commit convention**: read recent `git log --oneline -10` to detect pattern

### 3. Confirm with the user

Present what you detected and ask for corrections. One question at a time:

1. **Issue tracker** — `github` / `jira` / `linear` / other
2. **Tracker-specific config** — for Jira: project key + base URL; for Linear: team key; for GitHub: nothing extra
3. **Test command** — e.g. `pnpm test`, `make test`, `pytest`
4. **Commit convention** — `conventional-commits` / `repo-style` (inferred from history) / other

### 4. Write AGENTS.md

Write to `AGENTS.md` in the repo root using the template below. Do not overwrite sections the user said to skip.

<agents-template>
## Issue Tracker
type: <github|jira|linear>

## Issue Tracker Commands
create: <command to create an issue — use $TITLE, $BODY, $LABEL as placeholders>
view: <command to view issue $ID>
close: <command to close issue $ID>
list: <command to list open issues>

## Test Command
test: <test command>

## Commit Convention
convention: <conventional-commits|repo-style>
</agents-template>

**GitHub example:**
```
create: gh issue create --title "$TITLE" --body "$BODY" --label "$LABEL"
view:   gh issue view $ID
close:  gh issue close $ID
list:   gh issue list --state open
```

**Jira example:**
```
create: jira issue create --project $PROJECT --summary "$TITLE" --description "$BODY"
view:   jira issue view $ID
close:  jira issue transition $ID "Done"
list:   jira issue list --project $PROJECT --status "To Do"
```

**Linear example:**
```
create: linear issue create --title "$TITLE" --description "$BODY" --team $TEAM
view:   linear issue view $ID
close:  linear issue update $ID --state "Done"
list:   linear issue list --team $TEAM --state "Todo"
```

### 5. Symlink skills

```bash
mkdir -p .claude/skills
for skill in .skills/skills/*/; do
  name=$(basename "$skill")
  ln -sf "../../$skill" ".claude/skills/$name"
done
```

Report which skills were linked. Confirm `AGENTS.md` was written.
