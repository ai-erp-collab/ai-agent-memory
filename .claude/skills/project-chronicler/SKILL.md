---
name: project-chronicler
description: Automatic update of architecture documentation in docs/project.md after any code changes.
---

# Project Chronicler Skill

## When to Activate
At the end of all planned changes or before ending a session.

## Steps
1. **Analyze changes:** Scan the changes made (current buffer or file structure).
2. **Categorize:**
   - If a file was added → update the "Module Registry" section.
   - If `package.json` / `requirements.txt` changed → update "Stack".
   - If module interaction logic changed → update "Architecture".
3. **Sync:** Open `docs/project.md` and apply edits, preserving the structure.

## Reference Structure for docs/project.md
Make sure the file always contains:
1. **Description:** 2-3 sentences about the essence of the project.
2. **Current Stack:** Versions of key technologies.
3. **Architecture:** Description of patterns (e.g. Clean Architecture, Event-driven).
4. **Module Registry:** Table: Module Name | Responsibility | Dependencies.
5. **Onboarding Tips:** The most important nuances for a "new" AI agent.
