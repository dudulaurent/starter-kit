# Grill context

Read by the `grill-with-docs` skill. It says where this vault keeps its glossary and decisions.

- Glossary for vault-wide terms: `wiki/CONTEXT.md`
- Glossary for one agent's terms: `agents/[name]/wiki/CONTEXT.md` (agent terms stay in the agent)
- Decisions: `wiki/adr/` for cross-agent decisions, `agents/[name]/wiki/adr/` for one agent
- Loading rule: in an Agent Session load the agent glossary first, then the vault glossary.
  In a Root Session load only the vault glossary.
- Authority document: none
