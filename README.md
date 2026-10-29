# Vault starter kit

A personal knowledge vault that an AI coding agent maintains for you, built on the LLM Wiki pattern. It works with Claude Code and with Codex: the agent keeps structured markdown notes up to date, so what you learn and decide accumulates instead of being worked out again every conversation.

This kit contains everything needed to set one up. It carries no personal content from the person who made it.

## What is in the box

| File or folder | What it is |
|---|---|
| `vault-guide.html` | A visual guide. Open it in a browser. It explains the structure, how the pieces link, how a session works and the vocabulary. Start here. |
| `vault-template/` | Path A. A ready skeleton: copy it, open your agent in it, and fill the blanks. |
| `SETUP.md` | Path B. A staged guide for your agent that builds the vault by interviewing you, across several sittings. |

## Two paths

**Path A: template folder (faster, you edit).**
1. Copy `vault-template/` to where you want your vault. Run `git init` in it.
2. Open it as a vault in Obsidian (optional) and open a terminal in the folder.
3. Start Claude Code or Codex there and say: *"Read AGENTS.md. Then walk me through filling every `<placeholder>` in me/ and the example agent, one question at a time, and replace the example agent with mine."*
4. Close the session, open a new one, and start the routine: type `/session-start` in Claude Code or `$session-start` in Codex.

**Path B: setup guide (slower, the agent builds).**
1. Make an empty folder and open Claude Code or Codex in it.
2. Attach `SETUP.md` or paste its contents and say: *"Follow this guide. Start at Stage 0."*
3. It works through seven stages and keeps a progress file, so you can stop and resume in a later session.

Choose A if you already know what you want. Choose B if you would rather be interviewed and let the structure follow your answers.

## Which file does my tool read?

| | Claude Code | Codex |
|---|---|---|
| Rules | `CLAUDE.md` (a one-line pointer to `AGENTS.md`) | `AGENTS.md` |
| Skills | `.claude/skills/` | `.agents/skills/` |
| Start the routine | `/session-start` | `$session-start` |

The skills exist in both folders because each tool only looks in its own. Everything else is shared. Edit `AGENTS.md`, never the pointer.

## Requirements
- Claude Code or Codex (terminal, desktop app or editor extension)
- Git
- Obsidian, optional, for browsing the notes

## The idea in five lines
1. A **vault** is a folder. **Agents** are named areas inside it, each with one job.
2. Every session starts with the `session-start` routine and ends with `session-end`. Keep sessions short.
3. Facts have three homes: the item's record, one line on the dashboard, or a lesson in the patterns file.
4. The agent writes, you talk. Big files change only after your yes.
5. Anything bigger than a tweak is questioned first with `grill-with-docs`.

## Going further
Once the loop is stable you can add code agents with a tickets board and build roles, peer projects with their own repo, a shared plugin repo for routines used in several projects, and guards that block mechanical mistakes. `vault-guide.html` shows where each of these fits.
