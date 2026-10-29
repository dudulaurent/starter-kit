# Example Ops Agent: Operational Configuration
*Stacks on top of the vault root: ../../AGENTS.md*
*Global rules (write and ask model, confidentiality, narrative drift, session protocol) live there.*

## What this agent does
<One paragraph: the domain, the job, who benefits. Replace this whole agent with your own.>

## Shared resources
Relative paths from this agent's working directory:

→ Identity and values: ../../me/identity.md
→ Master experience: ../../me/profile.md
→ Working preferences: ../../me/preferences.md
→ Current state: dashboard.md (agent root)
→ Session continuity: last-session.md (agent root), overwritten at each session end
→ Open threads: threads/active/, one file each with frontmatter
→ Wiki hub: wiki/example-ops-agent-wiki.md
→ Immutable source documents: raw/

## Work items
This agent calls its unit of work an **Item**. Active items live in `items/active/`, finished
ones in `items/done/`, and `items/board.md` lists them with one line each. When an item moves,
update the board in the same step.

## Session additions
<Optional extra steps for session-start and session-end in this agent. Delete if none.>

## What does NOT belong here
Current status and item outcomes. Those live in the dashboard and item records.
