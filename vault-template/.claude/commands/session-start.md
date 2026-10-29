---
description: Context-loading sequence. Run before any other work in a session.
---

# /session-start

Run before any other work. Read `.claude/session-context.md` first for this vault's nouns and paths.

## Step 1: Detect session type
- **Agent Session**: the working directory is inside `agents/[name]/`.
- **Root Session**: the working directory is the vault root. Skip the agent-only steps below.

## Step 2: Load state
1. Read the vault index `dashboard.md` at the root. It is short and names the active agents.
2. **Agent Sessions:** read the agent's `dashboard.md`, then `last-session.md`, then `wiki/patterns.md`.
3. **Agent Sessions:** read the agent's board (`items/board.md`) for one line per item.

Never read another agent's dashboard. If you are loading a sibling's content, a path is wrong.

## Step 3: Reconcile concurrent and human edits
Run `git fetch`, `git status --branch` and `git log --oneline -5`. Another session may have
landed work, and the owner may have edited a file directly. If any change touches an
agent-maintained file (dashboard, items, threads, wiki), read it and reconcile before writing.

List branches ahead of `main` and say whether each holds work:

```
git branch --format='%(refname:short)' | while read b; do
  [ "$b" = main ] || echo "$b: $(git rev-list --count main..$b) commits ahead"
done
```

## Step 4: Load the wiki nav
**Agent Sessions:** read `wiki/[name]-wiki.md`, the navigation hub of the agent.

## Step 5: Scan threads and items
Scan `threads/active/` and `items/active/`. Note anything overdue or blocking.

## Step 6: Run agent-specific start checks
If the agent's CLAUDE.md defines any under "Session additions", run them. Root Sessions skip this.

## Step 7: Confirm
Print a short summary: session type and agent, active priorities from the dashboard, open
threads and items, any concurrent edits found, any urgent item. Do no other work until this is done.
