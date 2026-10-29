---
name: grill-with-docs
description: Interview session that challenges a plan against the vault's glossary and past decisions, sharpens terms, and records resolved terms and decisions as it goes. Use before building any new agent, project or significant feature.
---

# Grill with docs

Interview the owner about every part of the plan until you share the same understanding. Walk
down each branch of the design, resolving dependencies between decisions one at a time. For each
question, give your recommended answer and the reason. Ask one question at a time and wait.
If the answer is in the files, read the files instead of asking.

## Where things live
Read `vault-config/grill-context.md`. It names the glossary (`CONTEXT.md`) and the decisions folder
(`adr/`) for this vault. Create files only when there is something to write.

## During the session
- **Challenge against the glossary.** If a term conflicts with the glossary, say so at once.
- **Sharpen fuzzy language.** Propose one precise term when the owner uses a vague or overloaded word.
- **Use concrete scenarios.** Invent edge cases that force the boundaries between concepts to be exact.
- **Cross-check the files.** If the owner says one thing and the files say another, surface it.
- **Write terms as they are resolved**, not at the end. CONTEXT.md is a glossary only. It holds no
  implementation detail.

## Offer an ADR only when all three are true
1. Hard to reverse: changing your mind later costs real effort.
2. Surprising without context: a future reader will ask why.
3. A real trade-off: there were genuine alternatives and one was chosen for stated reasons.

ADR format: one file `NNNN-short-slug.md` with Status, Context, Decision, Consequences.

## Before closing, the mandatory checkpoint
1. Is every term resolved this session written to CONTEXT.md?
2. Does each qualifying decision have an ADR, or an explicit reason it does not?

Do not close the session until both are answered.
