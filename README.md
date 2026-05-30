# Multi-level Memory Template for Claude Projects

A project structure template that gives Claude persistent memory across sessions. Four levels of information storage — from the current task to an accumulated knowledge base.

---

## Concept: Memory Levels

```
┌─────────────────────────────────────────────────────────┐
│  LEVEL 1 — SESSION (SESSION_STATE.md)                   │
│  What we're doing, what's done, what not to touch.      │
│  Updated EVERY session before saying "done".            │
├─────────────────────────────────────────────────────────┤
│  LEVEL 2 — PROJECT (docs/project.md)                    │
│  Stack, modules, API, test status.                      │
│  Updated on major architecture changes.                 │
├─────────────────────────────────────────────────────────┤
│  LEVEL 3 — WIKI (docs/wiki/)                            │
│  Decisions, concepts, research — accumulates over time. │
│  Read on demand, not in full.                           │
├─────────────────────────────────────────────────────────┤
│  LEVEL 4 — PERSISTENT (memory/ → ~/.claude/...)         │
│  Insights, preferences, patterns — across sessions.     │
│  Index in MEMORY.md, details in separate files.         │
└─────────────────────────────────────────────────────────┘
```

**Principle:** Claude reads only what it needs. Session — always, wiki — on demand only.

---

## Template Files

| File | Where to copy | What to do |
|------|---------------|------------|
| `CLAUDE.md` | project root | fill in commands, stack, rules |
| `SESSION_STATE.md` | project root | update every session |
| `docs/project.md` | `docs/project.md` | describe the architecture |
| `docs/known-issues.md` | `docs/known-issues.md` | log traps and pitfalls |
| `docs/wiki/` | `docs/wiki/` | structure for accumulated knowledge |
| `memory/MEMORY.md` | `~/.claude/projects/<PROJECT>/memory/` | memory index |
| `memory/project.md` | next to MEMORY.md | project context |

---

## Skills (`.claude/skills/`)

Two skills for project memory support:

| Skill | Purpose | When to invoke |
|-------|---------|----------------|
| `archivarius` | Wiki and knowledge base management | Add a document, search the base, update a page, audit |
| `project-chronicler` | Auto-update `docs/project.md` | At end of session when code has changed |

Skills are invoked via the `Skill` tool in Claude Code. No configuration needed — Claude finds them automatically from `.claude/skills/`.

---

## How MEMORY.md Works

`memory/` is Claude Code's native auto-memory. Claude Code automatically loads the contents of `~/.claude/projects/<PROJECT>/memory/` into the context of every new session — no skills or configuration required.

**Folder structure:**
```
memory/
├── MEMORY.md       # index — loaded first, max 200 lines
└── project.md      # example memory entry (add your own files)
```

**Memory file format** — frontmatter + body:
```markdown
---
name: project-context
description: Project context — stack, decisions, focus
metadata:
  type: project
---

Entry content...
```

**Entry types** (`metadata.type`):
- `user` — user preferences and working style
- `feedback` — what to do / avoid in this project
- `project` — current status, decisions, constraints
- `reference` — where to find information (Linear, Slack, Grafana, etc.)

**What Claude does automatically:**
- Saves new entries when it learns something important about the project or user
- Updates stale entries
- Indexes them in `MEMORY.md`

**What not to store in memory/:** anything already in the code, git history, or SESSION_STATE.md — only what's not obvious from project files.

---

## How to Set Up Persistent Memory

1. Determine the memory path for your project:
   ```
   C:\Users\<USER>\.claude\projects\<PROJECT-PATH-SLUG>\memory\
   ```
   where `<PROJECT-PATH-SLUG>` is the project path with `\` → `-` and `:` removed.

   Example: `E:\Projects\MyApp` → `E--Projects-MyApp`

2. Copy `memory/MEMORY.md` and `memory/project.md` there

3. Set the path in your project's `CLAUDE.md` (section "Persistent Memory")

---

## Claude's Workflow in a Session

```
Session start
    ↓
Reads SESSION_STATE.md (level 1)
    ↓
Reads docs/known-issues.md (traps)
    ↓
If needed: docs/project.md (level 2)
    ↓
If needed: docs/wiki/ (level 3)
    ↓
Works on the task
    ↓
New trap found → appends to known-issues.md
    ↓
End of session → updates SESSION_STATE.md + memory/
```

---

## Rules That Actually Work

- **Before coding** — read `known-issues.md`. Saves hours.
- **End of session** — update `SESSION_STATE.md` without fail. Otherwise the next session starts from scratch.
- **Don't read the wiki in full** — just `SESSION_STATE + project.md`. Details on demand.
- **Context ~5% before compression** — update `SESSION_STATE.md` → update `docs/project.md` → `/clear`
