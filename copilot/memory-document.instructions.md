---
applyTo: **/*
---
# Memory Document

## Scope
- File: project root `.agent_memory.md`. Single source; create if missing.
- On task start: read `.agent_memory.md` if present; apply Design / Logging / Developer instructions / APIs.

## When to write
- Design decision or constraint agreed or implemented.
- Developer instructs usage (logging, workflow, tool).
- Context7 (or similar) used for an API; add minimal usage if central or user-referred repeatedly.
- User repeatedly specifies an API or pattern: add or refresh entry.

## Format
- AGENT READABLE: headings + lists + code only; one line per fact; no prose.
- APIs: `import or usage` — one-line note; no long examples.

## Sections (use only if content exists)
- **Design**: one-line constraints/decisions; `[Module]: role or invariant`.
- **Logging**: how to log (module, level, format); where logs go.
- **Developer instructions**: what to always do; tool/workflow command or step.
- **APIs**: `**[Lib]**` `snippet` — one-line when/gotcha.

## Rules
- Update existing bullet over duplicate; remove obsolete; one to two lines per API.
- On user correction of API or pattern: update `.agent_memory.md` immediately.
