---
applyTo: **/idea.md
---

# IDEA Standards (Concepts & Terminology)

## 1. Purpose
- State the problem this module addresses and why it exists.
- Exclude implementation, interfaces, commands, and code.

## 2. Role in System (static position)
- One sentence: where this module fits in the whole system.
- Inputs and outputs at the concept level (names only).
- Upstream/downstream modules (names only).

## 3. Core Concepts
- For each concept, add one entry using this schema:
  - Name: <ConceptName>
  - Definition: one-sentence meaning in this context
  - Why it matters: the decision/behavior it enables
  - Scope: what is included
  - Non-goals: what is explicitly excluded

## 4. Boundaries & Responsibilities (ownership)
- Responsibilities this module owns (what it must do).
- Responsibilities explicitly not owned (what it must not do).
- Constraints this module enforces.

## 5. Conceptual Workflow (internal flow)
- High-level steps from input to output within this module.
- Data transformations at the concept level inside this module.
- Methods/techniques used at the concept level (names only).
- Decision criteria for choosing among methods under different conditions.

## 6. Interactions with Other Modules (contracts)
- Conceptual contracts for exchanged data (names and meanings only).
- Dependencies and assumptions on neighboring modules/components.
- Shared terminology to avoid duplication or drift.

## 7. Scenarios (behavioral examples)
- Typical: observable outcome under normal inputs.
- Boundary: behavior at limits (missing input, conflicting signals).
- Interaction: cross-module behavior using the contracts above.

## 8. Assumptions & Constraints
- Preconditions required for inputs and environment.
- Postconditions guaranteed on outputs.
- Invariants that must always hold for correctness (concept level).
- Resource, ordering, and timing constraints (concept level only).

## 9. Agent Outputs (when generating human docs)
- Produce a minimal glossary from Core Concepts entries (Name, Definition, Why it matters).
- Include a conceptual diagram of Role in System and Interactions.
- Provide 2–3 scenario write-ups (Typical, Boundary, Interaction) as prose.
- Link to `design.md` for design details once defined.
