# Vault: Root Instructions

## What this is
This is <OWNER NAME>'s personal Obsidian vault, used as a persistent wiki and knowledge base.
It follows the LLM Wiki pattern: the agent incrementally builds and maintains structured
markdown files instead of re-deriving knowledge on every question.

The vault is designed to host several agents, each with its own folder under `agents/`.

## Active agents
<!-- One line per agent. Add a line when you create an agent, remove it when you retire one. -->
→ Example ops agent: [[agents/example-ops-agent/AGENTS.md]]

## Identity
→ Who the owner is, values and background: [[me/identity.md]]
→ Experience and achievements: [[me/profile.md]]
→ Working preferences: [[me/preferences.md]]
At the start of every session, read `me/identity.md` before anything else.

## Vault map
→ Which agents are active and what blocks: [[dashboard.md]] (an index only)
→ Session continuity: `last-session.md` per agent, overwritten at each session end
→ Open threads: `agents/[name]/threads/active/` per agent, `threads/active/` for the vault itself
→ Architecture decisions: [[wiki/adr/adr-index]]
→ Vault vocabulary: [[wiki/CONTEXT.md]]
→ Immutable source documents: `agents/[name]/raw/`

## Rules
→ Communication style and voice: [[vault-config/rules/communication-style.md]]
At the start of every session, read `vault-config/rules/communication-style.md` and follow it
in every reply and every file you write. Keep sessions short: the voice rules are read once
and fade in a long conversation, so start a fresh session when a session grows long.

## Global behavioral rules

### The agent writes, the human talks
The agent is the only one who writes to the vault. The human does not edit files directly.
- Routine updates (status, outcomes, new items): the agent asks structured questions, then writes.
- Major files (this file, `me/profile.md`, `me/identity.md`): the agent shows the exact change
  and waits for an explicit yes before writing.

### Confidentiality
Never share or reference personal data outside the vault context.

### Narrative drift
When what the owner says in conversation differs from `me/` or an agent's narrative file,
ask a question instead of silently updating.

### Session start (all agents)
Run the `session-start` skill. This vault's nouns and paths are in
`vault-config/session-context.md`.

### Session end (all agents)
Run the `session-end` skill.

### Brainstorming and new features
Before building a new agent, project or large feature, run the `grill-with-docs` skill. It
challenges the plan against the vault's vocabulary and past decisions before anything is created.

### Pattern propagation
When you notice a habit in one agent that could help the others, tell the owner and propose a
scope (Vault, Code or Ops). Write it to `wiki/patterns.md` only after an explicit yes.
Run the `lint-vault` skill weekly from a Root Session to review pending patterns.

### Concurrent sessions
Two sessions can run at once. Each session works on its own branch, stages explicit file paths
(never `git add -A`), and never pushes to `main` without the owner's explicit yes. Re-read
`dashboard.md` and `last-session.md` before editing, since another session may have changed them.

## What does NOT belong in this file
Application status, work-item outcomes, targets, anything that changes weekly. Those live in
the agent wikis and dashboards. If this file needs weekly edits, the content is in the wrong place.

## This file changes when
- The owner's identity or core expertise shifts (rare)
- A new global behavioral rule is established
- A new agent is added (add a pointer under Active agents)
