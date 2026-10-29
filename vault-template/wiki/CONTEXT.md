# Vault

<OWNER NAME>'s personal Obsidian workspace: a persistent knowledge base and multi-agent system
built on the LLM Wiki pattern.

## Language

**Vault**:
The root workspace. Contains all Agents, the Vault index and the shared configuration.
_Avoid_: Repo, workspace

**Agent**:
A named configuration with one domain and purpose, with its own instruction file, wiki, dashboard and
threads. Reports state to its own dashboard and `last-session.md`.
_Avoid_: Project (ambiguous), bot

**Instruction file**:
The one file holding the rules for the Vault or for one Agent, loaded by the AI tool on its own.
An Agent's instruction file stacks on top of the Vault's. It points to the owner's identity and
voice files and does not copy them.
_Avoid_: Config, prompt, rules file

**Wiki**:
The structured knowledge base inside one Agent: a navigation hub, reference files, decisions.
_Avoid_: "The wiki" for the whole vault

**Dashboard**:
One file per Agent holding only what is true right now. Trimmed at every session end.
_Avoid_: Status file

**Vault index**:
The root `dashboard.md`. A thin list of active Agents and anything blocking.
_Avoid_: Master dashboard

**Session**:
One conversation with an AI coding agent, with a start routine (`session-start`) and an end
routine (`session-end`). Scoped to one Agent (Agent Session) or the vault root (Root Session).

**Work item**:
The unit of work an Agent tracks. Each Agent names it (Ticket, Application, Task). Its record
file holds the full story of that item.

**Thread**:
An open follow-up saved as its own file in `threads/active/`, with frontmatter
(`type: thread`, `status`, `title`, `created`, optional `due`).

**Three homes**:
The rule for where a fact is saved: the item's own record, the dashboard (one line), or the
agent's `wiki/patterns.md` (a lesson that held twice).

**Pattern**:
A habit or convention that proved useful in one Agent and may help others. Proposed to the
owner, recorded in `wiki/patterns.md` only after approval.

**Command / Skill**:
Both are skills in the tools' own terms. A Command is a named routine the owner can start by
typing its name (`session-start`). The agent may start it too when the vault's instructions tell
it to. A Skill is a helper the agent picks up when the task matches (`grill-with-docs`).
_Avoid_: Describing a Command as something only the owner can start

## Flagged ambiguities
- "Command" was used to mean "only the owner can start it". Resolved: it means a named routine
  the owner can type, and the agent may start it as well. Who may start a skill is a setting on
  that skill, not a separate kind of thing.
