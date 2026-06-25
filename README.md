# Skills

Dev workflow skills for Claude Code and Antigravity. Adapted from [mattpocock/skills](https://github.com/mattpocock/skills) and [EveryInc/compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin).

## Skills

| Skill        | Description                                                                        |
| ------------ | ---------------------------------------------------------------------------------- |
| `/ideate`    | Stress-test a plan through Socratic dialogue before committing to a direction      |
| `/prd`       | Synthesize the conversation into a PRD and write it to `docs/prd/`                |
| `/breakdown` | Break a PRD or feature into vertical-slice issues                                  |
| `/tdd`       | Implement a feature or issue test-first via red-green-refactor                     |
| `/review`    | Two-axis review — Standards (conventions) and Spec (matches the issue/PRD?)        |
| `/refactor`  | Plan a refactor via interview, break into tiny safe commits, file an issue         |
| `/research`  | Quick focused lookup — codebase patterns, library APIs, where something is defined |
| `/wrap`      | End-of-session sync — update memory, skill files, CLAUDE.md, and issue states      |
| `/commit`    | Stage and commit with a well-crafted conventional commit message                   |
| `/debug`     | Systematic diagnosis and fix — triage, root cause, test-first fix                  |
| `/pr`        | Commit, push, and open a PR with a well-crafted description                        |

## Install

```bash
npx skills add utsabbera/skills
```

Works with Claude Code, Antigravity, Codex, Cursor, and [70+ agents](https://skills.sh). No registration required — any public GitHub repo works.

Installs to the project by default (`.claude/skills/`). Use `-g` for global (`~/.claude/skills/`):

```bash
npx skills add utsabbera/skills -g
```

Pick specific skills with `--skill`, or install all:

```bash
npx skills add utsabbera/skills --skill tdd --skill review --skill commit
```

Use `--copy` if you want to modify skills locally (otherwise symlinked):

```bash
npx skills add utsabbera/skills --copy
```

## AGENTS.md

Skills read your project's `AGENTS.md` to adapt to its tooling. Add these keys for full integration:

```md
## Issue Tracker Commands
create: gh issue create --title "$TITLE" --body "$BODY" --label "$LABEL"
view:   gh issue view $ID
close:  gh issue close $ID
list:   gh issue list --state open

## Test Command
test: pnpm test
```

Skills fall back to `gh` if these keys are absent. Supported trackers: GitHub, Jira, Linear.
