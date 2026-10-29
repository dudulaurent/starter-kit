# Vault setup guide for Claude

*Path B: attach or paste this file into Claude Code, opened in an empty folder. It builds a personal Obsidian vault in stages across several sessions. Path A (the `vault-template/` folder) gives you the finished skeleton at once. Both end in the same vault.*

## Instructions to Claude

You are setting up a personal knowledge vault for the person you are talking to, called the owner below. The vault follows the LLM Wiki pattern: you maintain structured markdown files so knowledge accumulates instead of being re-derived each time. Read this whole file before doing anything.

### Ground rules for the setup
1. **Work in stages, one stage per sitting if needed.** A full vault does not fit in one session and should not be rushed. Finish a stage, then stop and offer to continue.
2. **Keep a progress file.** Create `SETUP-PROGRESS.md` in the vault root after Stage 0. Tick each stage when done and note decisions the owner made. At the start of every later session, read it first and resume at the first unticked stage.
3. **Ask, then write.** Ask one question at a time. For each question give a recommended answer and the reason. Show at least three options whenever the owner must choose.
4. **Plain language.** Explain every technical choice in everyday terms before any jargon.
5. **Show before major writes.** Before writing `.claude/CLAUDE.md`, `me/identity.md` or `me/profile.md`, show the exact text and wait for a yes.
6. **No invented facts.** If the owner has no number for an achievement, record it qualitatively.
7. **Git hygiene.** Initialise git at Stage 0. Commit at the end of every stage, staging explicit paths only.

### Stage 0: Orientation (10 minutes)
- Check the folder is empty or confirm what is in it. Run `git init` if needed.
- Ask: the owner's name, preferred language for replies, and whether they use Obsidian already (the vault is plain markdown, so Obsidian is optional but recommended for browsing).
- Ask what they want the vault for. Offer at least three typical uses, for example a job search, a learning and research base, a side project with code, a household or family system, a business operations log. They may pick several. Each use becomes an agent later.
- Create `SETUP-PROGRESS.md`, then explain in five sentences the model below ("The model") so the owner knows what they are building.

### Stage 1: Identity (one sitting)
Interview the owner to fill three files. Show each draft before writing it.
- `me/identity.md`: background, current focus, what is distinctive, values, languages.
- `me/profile.md`: roles, education, skills, projects, each with concrete evidence.
- `me/preferences.md`: reply length, how decisions are presented, tools and formats, things to always ask first, things never to do.

Then derive `.claude/rules/communication-style.md` from how the owner writes and what they dislike. Offer the example rules (concise, minimum 3 options, plain language first, no filler) and let them keep, drop or add.

### Stage 2: Skeleton (one sitting)
Create the folder structure and shared files exactly as listed under "Target structure". Write real content, not empty stubs, for:
- `.claude/CLAUDE.md`: what the vault is, active agents, identity pointers, vault map, global behaviour rules (agent writes and human talks, confidentiality, narrative drift, brainstorm gate, pattern gate, concurrent sessions), what does not belong in the file.
- `.claude/session-context.md`: the two session types and the nouns and paths table.
- `.claude/grill-context.md`: where glossary and decisions live.
- `.claude/commands/session-start.md`, `session-end.md`, `lint-vault.md`: the three routines.
- `.claude/skills/grill-with-docs/SKILL.md`: the interview skill.
- `dashboard.md` (the vault index), `last-session.md`, `wiki/CONTEXT.md`, `wiki/patterns.md`, `wiki/adr/adr-index.md`.

Use the descriptions in "What each shared file does" for their content. Commit. Tell the owner to close the session and open a new one at the vault root, so the commands load.

### Stage 3: First agent (one or two sittings)
Open a new session at the vault root and run `/session-start`. Then run the `grill-with-docs` skill on the owner's first use case. The interview should settle: the agent's name, its job in one sentence, what its work item is called, what raw material it reads, what it must never do without asking. Then create `agents/<name>/` with the layout under "Anatomy of an agent". Record any resolved term in `wiki/CONTEXT.md`. Offer an ADR only if the decision is hard to reverse, surprising without context and a real trade-off.

End the sitting with `/session-end` to prove the loop works.

### Stage 4: Prove the loop (one sitting)
Do real work in the new agent for one session. At the end, run `/session-end` and inspect the result together with the owner: was the dashboard trimmed, did the right facts land in the right home, is `last-session.md` useful? Fix the commands where they fell short. The aim is for the owner to trust the loop before adding more.

### Stage 5: Grow (as needed, any order)
- **Another agent.** Repeat Stage 3. Add it to the root dashboard, CLAUDE.md and session-context.
- **A code agent.** For an agent that owns software, add tickets (`tickets/active`, `tickets/done`, a board), a build context file, and a build routine with separate roles: spec, design, build, quality. Keep role definitions in `.claude/agents/`.
- **A peer project.** A project that needs its own git remote lives beside the vault, not inside it. The vault index points at it and never loads its content.
- **Shared framework.** When two or more repos need the same commands, move them into a Claude Code plugin marketplace repo and install it in each. Not before.
- **Guards.** Once the habits are stable, add hooks that block mechanical rule breaks, for example pushing to `main` or staging everything.

### Stage 6: Share (optional)
Generate an atlas page (a single HTML file) that shows the structure with the owner's agents. Keep it to structure only: no names, outcomes, figures or private material.

---

## The model

A **vault** is a folder of markdown files. Inside it, **agents** are named areas, each with one job, its own instructions, notes, current state and follow-ups. You open Claude Code in a folder, and the instructions in that folder tell Claude which role to play and what to read. Three habits make it compound:

1. **Every session starts and ends the same way.** Start loads the current state. End writes what changed to the right place.
2. **Facts have three homes.** About one item: its own record. True right now: one line on the dashboard. A lesson that held twice: the patterns file.
3. **The agent writes, the human talks.** Claude is the only editor. For the big files, Claude shows the change and waits for a yes.

## Target structure

```
vault/
├── .claude/
│   ├── CLAUDE.md                 root rules, loaded in every session
│   ├── session-context.md        nouns and paths for the two routines
│   ├── grill-context.md          where glossary and decisions live
│   ├── rules/communication-style.md
│   ├── commands/                 session-start, session-end, lint-vault
│   └── skills/grill-with-docs/SKILL.md
├── me/                           identity, profile, preferences
├── agents/
│   └── <agent>/
│       ├── .claude/CLAUDE.md     this agent's job and read-order
│       ├── dashboard.md          live state only
│       ├── last-session.md       overwritten each session end
│       ├── items/ (or tickets/)  active/, done/, board.md
│       ├── threads/              active/, done/
│       ├── raw/                  immutable source material
│       └── wiki/                 hub, CONTEXT.md, patterns.md, adr/
├── wiki/                         vault CONTEXT.md, patterns.md (registry), adr/
├── threads/                      vault-level follow-ups
├── ideas/                        early thoughts, before they earn an agent
├── dashboard.md                  the vault index, short
└── last-session.md
```

## What each shared file does

- **`.claude/CLAUDE.md`** is loaded automatically. It holds rules that apply to every agent. It must stay free of anything that changes weekly.
- **`session-context.md`** lets the two routines serve any vault: it names what a work item is called and where the board, dashboard and wiki hub are.
- **`session-start`** reads the vault index, then the agent's dashboard, last session, patterns and board. It runs `git fetch`, reconciles edits made by hand or by another session, lists branches ahead of `main`, scans threads, and prints a confirmation. It does no other work until done.
- **`session-end`** fetches again, updates the dashboard (deleting finished work), sorts each fact into its home, overwrites `last-session.md`, files threads, and commits on the session's own branch.
- **`lint-vault`** runs weekly from the vault root: checks that each agent has a glossary, proposes pending patterns, and checks that the index matches the agents folder.
- **`grill-with-docs`** interviews the owner before any new agent or feature and records resolved terms and decisions.
- **The vault index (`dashboard.md`)** lists active agents and anything that blocks across them. It carries no agent content, which keeps it cheap to load every session.
- **`wiki/CONTEXT.md`** is the glossary. **`wiki/adr/`** holds one file per hard-to-reverse decision.
- **`wiki/patterns.md` at root** is the registry of habits worth spreading between agents, written only after the owner approves.

## Anatomy of an agent

| Path | Purpose | Written when |
|---|---|---|
| `.claude/CLAUDE.md` | The agent's job, read-order, work-item name | Rarely |
| `dashboard.md` | What is true now, as short lines | Every session end |
| `last-session.md` | Summary and next priorities | Every session end, overwritten |
| `items/active`, `items/done`, `items/board.md` | Work item records and the one-line index | When an item opens, changes or closes |
| `threads/active`, `threads/done` | Open follow-ups, one file each | When a follow-up appears or resolves |
| `raw/` | Source documents, never edited | When new material arrives |
| `wiki/<agent>-wiki.md` | Navigation hub linking every wiki file | When a wiki file is added |
| `wiki/CONTEXT.md` | The agent's vocabulary | When a term is resolved |
| `wiki/patterns.md` | Lessons that held twice | At session end |
| `wiki/adr/` | The agent's own decisions | When a decision qualifies |

## Rules of thumb Claude should hold throughout
- Folder names stay stable. Renaming breaks every link, so name the work item per agent in prose and keep the folders.
- A thread is one open follow-up. A pattern needs two occurrences.
- An artifact of an item (a draft, a letter) files under that item, never beside it.
- Dashboards shrink. If one grows, the story belongs in an item record.
- `main` moves only when the owner says so.
