# skills

Dev workflow skills for Claude Code and Antigravity. Adapted from [mattpocock/skills](https://github.com/mattpocock/skills) and [EveryInc/compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin).

## Skills

| Skill | Description |
|---|---|
| `/brainstorm` | Stress-test a plan through Socratic dialogue before committing to a direction |
| `/prd` | Synthesize the conversation into a PRD, write to `docs/prd/`, and create a GitHub Issue |
| `/breakdown` | Break a PRD or feature into vertical-slice GitHub Issues |
| `/tdd` | Implement a feature or issue test-first via red-green-refactor |
| `/review` | Two-axis review — Standards (conventions) and Spec (matches the issue/PRD?) |
| `/refactor` | Plan a refactor via interview, break into tiny safe commits, file a GitHub Issue |
| `/research` | Quick focused lookup — codebase patterns, library APIs, where something is defined |
| `/wrap` | End-of-session sync — update memory, skill files, CLAUDE.md, and GitHub issue states |
| `/commit` | Stage and commit with a well-crafted conventional commit message |

## Install

### Claude Code (user-level)

```bash
for skill in skills/*/; do
  name=$(basename "$skill")
  ln -sf "$(pwd)/$skill" ~/.agents/skills/"$name"
done
```

### Antigravity

```bash
for skill in skills/*/; do
  name=$(basename "$skill")
  ln -sf "$(pwd)/$skill" ~/.antigravity/skills/"$name"
done
```
