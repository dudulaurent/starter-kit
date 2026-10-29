---
description: State-write sequence. Run at the end of every session before closing.
---

# /session-end

Read `.claude/session-context.md` for this vault's nouns and paths. Concurrency safety is
always on, because a session cannot tell whether a second one is running.

## Step 1: Fetch before assuming
Run `git fetch` and `git status --branch`. Another session may have landed work, and the
branch may not be the one this session started on.

## Step 2: Run agent-specific end steps
In an Agent Session, run the end steps in that agent's CLAUDE.md, if any. A Root Session has
none: say so plainly.

## Step 3: Update the dashboard
Dashboards hold live state only. Never append a recap. Delete what this session finished, add
what it opened, correct what it changed. Re-read the file before editing. Touch the root index
only if vault-level state changed.

## Step 4: Write history to the right home
Sort each fact by its kind, not by when it happened.

- **About one item** goes to that item's own record in `items/done/`.
- **True right now** goes to the dashboard as one line.
- **A lesson that generalises** goes to the agent's `wiki/patterns.md`. A single occurrence is a
  thread, not a pattern. It needs to have held twice.

If an existing dashboard entry names closed work in more than one line, collapse it to one line
in the same pass and move the story to the item's record. An artifact of an item (a draft, a
letter, a diagram) files under that item, never beside it.

## Step 5: Update last-session.md and threads
Overwrite `last-session.md` with a 1 to 2 sentence summary and numbered priorities for next
time. If another session wrote it since this one began, append a labelled section instead.
Create a thread file for each new open follow-up. Move resolved threads to `threads/done/`.

## Step 6: Checkpoint docs
If `grill-with-docs` ran, confirm the glossary has the resolved terms and that any qualifying
decision has an ADR.

## Step 7: Commit and push
1. Review `git status --short`. Stage explicit paths only. Never `git add -A` or `git add .`.
2. Run `git status --branch` immediately before committing.
3. Commit with a message naming what was done.
4. Check `git log --oneline -1` after.
5. Push this session's own branch. Do not merge to `main` unless the owner asked in this session.

## Step 8: Confirm
State which files changed and what changed in each, so the owner can verify without opening them.
