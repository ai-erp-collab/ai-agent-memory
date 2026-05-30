# Wiki — Project Knowledge Base

The wiki accumulates knowledge that doesn't fit in `project.md`. Read on demand, not in full.

## Structure

```
docs/wiki/
  decisions/    ← architecture decisions (why we did it this way)
  concepts/     ← key domain concepts
  research/     ← technology and approach research
  analysis/     ← analytics, benchmarks, experiments
```

## How to Write a Decision

```markdown
# Decision: [Name]

**Date:** YYYY-MM-DD
**Status:** accepted / rejected / under discussion

## Context
What required a decision.

## Options
- Option A: ...
- Option B: ...

## Decision
We chose A because...

## Consequences
What this means for the code/architecture.
```

## How to Write a Concept

```markdown
# Concept: [Name]

What it is and why it's needed in the context of the project.

## Key Properties
- ...

## How It's Used in the Project
...
```
