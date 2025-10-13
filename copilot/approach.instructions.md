---
applyTo: **/idea.md
---
# IDEA Standards (Concepts & Terminology)

## Required Document Structure
The following sections MUST appear in every idea document:

### 1. Context
- Problem
- Role in system (one sentence)
- Inputs (concept names)
- Outputs (concept names)
- Upstream modules (names)
- Downstream modules (names)
- Exclude implementation, interfaces, commands, code

### 2. Goals
- Goals (outcomes at concept level)
- Non-goals (out of scope)
- Responsibilities owned
- Responsibilities not owned
- Success criteria (concept level)

### 3. Concepts
- Concept diagram of module position and interactions
- For each concept:
  - Name
  - Definition
  - Why it matters
  - Scope
  - Non-goals

### 4. Contracts & Flow
- Contracts for exchanged data (names, meanings)
- Internal steps from input to output
- Data transformations (concept level)
- Methods/techniques (names only)
- Decision criteria for method choice
- Dependencies on neighboring modules
- Assumptions about neighboring modules
- Shared terminology

### 5. Scenarios & Constraints
- Scenarios: Typical, Boundary, Interaction
- Preconditions
- Postconditions
- Invariants
- Resource, ordering, timing constraints

---

## AI Generation Guidelines (Internal Use Only)

### Content Focus
- Concepts and terminology only
- Exclude implementation details, APIs, commands, code samples
- Link to design.md for technical specifications

### Writing Style
- Clear and concise language
- No redundant information
- Audience: Researchers and Developers
- Consistent terminology across modules

### Diagram Requirements
- Concept diagrams of module relationships
- Simple visual structure
- Show data flow and interactions

### Scenario Development
- Observable examples
- Include normal, boundary, interaction cases
- Consistent terminology
- Demonstrate key concepts