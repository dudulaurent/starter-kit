# Session context: vault root

Read by `/session-start` and `/session-end`. It names this vault's nouns and paths so the two
commands do not have to hardcode them.

## The two session types

- **Root Session**: the working directory is the vault root. No agent is active. Used for
  vault-level work: the pattern registry, cross-agent decisions, `/lint-vault`, adding an agent.
- **Agent Session**: the working directory is inside `agents/[name]/`. The agent's own folder
  supplies the dashboard, threads and wiki that the commands expect.

## Nouns and paths

| Thing | Here |
|---|---|
| Work item | Item (rename per agent: Ticket, Application, Task, Note) |
| Active items | `agents/[name]/items/active/` |
| Done items | `agents/[name]/items/done/` |
| Board | `agents/[name]/items/board.md` |
| Dashboard | `agents/[name]/dashboard.md`. The vault root `dashboard.md` is an index only |
| Wiki nav | `agents/[name]/wiki/[name]-wiki.md` |
| Patterns | `wiki/patterns.md` at root is the pattern registry. `agents/[name]/wiki/patterns.md` holds that agent's own lessons |
| Threads | `threads/active/` at root. `agents/[name]/threads/active/` per agent |

Active agents: `example-ops-agent`. Update this line when you add or retire one.

## Session-start additions
None yet. Add vault-specific checks here, for example "list unmerged branches".

## Session-end additions
- **Root Session**: no agent-specific end steps. Touch the root `dashboard.md` only if
  vault-level state changed.
- **Agent Session**: run that agent's own end steps from `agents/[name]/.claude/CLAUDE.md`,
  then update the agent's own `dashboard.md`, `last-session.md` and `threads/`. Never write to
  another agent's files.
- Commit and push happen in `/session-end` step 7 and nowhere else.

## Authority document
None. `.claude/CLAUDE.md` holds the behaviour rules and `.claude/rules/communication-style.md`
holds the voice. Neither settles a domain dispute.
