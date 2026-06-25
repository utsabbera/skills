---
name: pr
description: Commit staged changes, push, and open a GitHub PR with a well-crafted description. Use when the user is ready to ship, says "open a PR", "push this", or "ship it".
---

Commit, push, and open a PR.

## Process

### 1. Gather context

Run: `git status`, `git diff HEAD`, `git branch --show-current`, `git log --oneline -10`

If the working tree is clean and all commits are pushed, skip to Step 4 to write the PR description for an existing branch.

### 2. Commit

Follow the same convention logic as `/commit`:
- Check `CLAUDE.md` or `AGENTS.md` for commit conventions first, then recent history, then default to conventional commits
- Scan for logical commit groups (file-level only, 2-3 max)
- Stage specific files, use heredoc format, no attribution lines

### 3. Push

```bash
git push -u origin HEAD
```

If on the default branch (`main`/`master`), create a feature branch first — derive the name from the change content.

### 4. Write the PR description

Infer the issue number from conversation context or branch name. Compose:

**Title**: conventional commit style, ≤72 chars, imperative mood

**Body**:
```
## What

[1-3 bullets: what changed and why — focus on the why]

## How to test

[Concrete steps to verify the change works]

## Closes

Closes #<N>  (omit if no issue)
```

Keep the body focused. No implementation details that belong in code comments.

### 5. Open the PR

Write the body to a temp file and pass via `--body-file` — never use `--body` with a heredoc directly:

```bash
BODY=$(mktemp) && cat > "$BODY" <<'EOF'
<body here>
EOF
gh pr create --title "<title>" --body-file "$BODY"
```

Report the PR URL.
