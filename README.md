# skills

Dev workflow skills for Claude Code and Antigravity. Adapted from [mattpocock/skills](https://github.com/mattpocock/skills) and [EveryInc/compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin).

Skills live at the **project level** — installed as a submodule so the whole team (and all agents) gets them on clone, versioned with the project, and adapted per-project via the existing `AGENTS.md`.

## Skills

| Skill        | Description                                                                        |
| ------------ | ---------------------------------------------------------------------------------- |
| `/setup`     | Pick which skills to install and symlink them into `.claude/skills/`               |
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
git submodule add https://github.com/<you>/skills .skills
```

Then run `/setup` to pick which skills to install. It reads your existing `AGENTS.md` and symlinks selected skills into `.claude/skills/`.

## AGENTS.md

Skills read your project's existing `AGENTS.md` to adapt to the project's tooling. Add these keys to enable full integration:

```md
## Issue Tracker Commands
create: gh issue create --title "$TITLE" --body "$BODY" --label "$LABEL"
view:   gh issue view $ID
close:  gh issue close $ID
list:   gh issue list --state open

## Test Command
test: pnpm test
```

Supported trackers out of the box: `gh` (GitHub), `jira`, `linear`. Skills fall back to `gh` if these keys are absent.
