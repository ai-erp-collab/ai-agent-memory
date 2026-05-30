# CLAUDE.md — [PROJECT NAME]

## Starting a New Session — Read in This Order

1. **`SESSION_STATE.md`** — where we are, what's next, what not to touch (read up to the `═══` marker)
2. **`docs/known-issues.md`** — traps for runs and tests (read before any code)
3. If architecture needed — **`docs/project.md`** (brief overview of modules and API)
4. If details needed — **`docs/wiki/`** (decisions, concepts, architecture)

> No need to read the wiki in full — `SESSION_STATE + project.md` is enough for most tasks.

---

## Key Commands

```bash
# TODO: add run, test, migration commands

# Tests
# python -m pytest tests/ -q

# Server
# python -m uvicorn app.main:app --host 127.0.0.1 --port 8000
```

---

## Where to Find Things

| Looking for | Where to look |
|---|---|
| Current status, tasks | `SESSION_STATE.md` |
| Traps and errors | `docs/known-issues.md` |
| Modules, API, test status | `docs/project.md` |
| Architecture decisions | `docs/wiki/decisions/` |
| Domain concepts | `docs/wiki/concepts/` |

---

## Stack (brief)

- **TODO:** fill in project stack
- **Backend:** ...
- **DB:** ...
- **Tests:** ...

---

## Session Rules

- **Before coding** — check `known-issues.md` for a similar trap
- **New problem found** — immediately append to `docs/known-issues.md`
- **End of session** — update `SESSION_STATE.md` (marker + tasks) before saying "done"
- **Context ~5% before compression** — propose: update `SESSION_STATE.md` → update `docs/project.md` → `/clear`

---

## Persistent Memory

Auto-memory: `C:\Users\<USER>\.claude\projects\<PROJECT-SLUG>\memory\`
- `MEMORY.md` — index
- `project.md` — architecture and status (update on major changes)

---

## Project Skills

Invoke via the `Skill` tool (do not read skill files with Read).

| Skill | When to invoke |
|---|---|
| `archivarius` | Any `docs/wiki/` operations: add a document, search the base, update a page, audit |
| `project-chronicler` | At end of session when code has changed — updates `docs/project.md` |

**Archivarius triggers:** "wiki", "knowledge base", "add to base", "write to wiki", "find in base", "ingest".
