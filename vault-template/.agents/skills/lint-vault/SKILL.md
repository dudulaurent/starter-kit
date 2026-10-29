---
name: lint-vault
description: Weekly vault health check and pattern propagation. Root Session only.
---

# lint-vault

Run weekly from a Root Session. Do not run from an Agent Session. It writes nothing without
the owner's approval for each step.

## Phase: documentation freshness
1. Check that `wiki/CONTEXT.md` exists at the vault root.
2. For each folder in `agents/`, check that `agents/[name]/wiki/CONTEXT.md` exists.
3. Flag any agent that has ADRs but no CONTEXT.md, since its vocabulary is missing.
4. Flag any agent CONTEXT.md untouched for 30 days while ADR activity continued.
5. Report, propose an action, and wait for the owner.

## Phase: pattern propagation
1. Read `wiki/patterns.md`, the pattern registry.
2. List every pattern whose status for some agent is `pending`.
3. For each, show the pattern, the target agent and the exact change you would make there.
4. Apply it only after the owner says yes to that step.
5. Record the adoption with a date in the registry (`adopted 2026-01-31`).

## Phase: index freshness
Check that the root `dashboard.md` lists every folder in `agents/` that is active, and that
`AGENTS.md` "Active agents" and `vault-config/session-context.md` agree with it. Check that each
folder holding an `AGENTS.md` also has a `CLAUDE.md` containing only `@AGENTS.md`.

## Rules
Never write without a per-step yes. Deprecated patterns move to the Archive section at the
bottom of the registry and are never deleted.
