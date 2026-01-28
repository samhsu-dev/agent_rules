---
applyTo: **/*
---

# Code Quality Standards

## Control Flow Optimization
- Prefer early returns over nested conditionals.
- Use guard clauses to minimize nesting and improve readability.
- Use `continue` to skip iterations instead of nested `if` blocks.
- Use `break` to exit loops when conditions are met.
- Keep logic flat and avoid deep nesting.

## Error Handling
- Catch specific exception types (avoid broad exception catching).
- Handle errors at the appropriate abstraction level.
- Preserve original exception context across call chains.
- Provide meaningful error messages.
- **Avoid silent fallback mechanisms**: raise exceptions instead of silently falling back to alternative implementations.
- **Fail fast**: raise exceptions immediately on initialization/operation failure; do not silently degrade functionality.
- **Exception-driven**: use exceptions to communicate errors; do not hide errors through fallback.
- **Never silent fallback**: do not silently return empty values (empty strings, empty lists, `null`/`None`) on failure. Log at appropriate level and raise or surface a clear error.

## Code Structure
- Keep functions short (ideally < 20 lines).
- Extract complex logic into dedicated functions.
- Avoid deep nesting (max 3 levels).
- Use meaningful variable and function names.

## Performance
- Use context managers for resource management/cleanup.
- Avoid unnecessary object creation in loops.
- Check caches before expensive operations.
- Optimize critical paths.

## Documentation
- Use English for comments and docs.
- Explain why (rationale) rather than what.
- **No historical notes**: do not include comments about code evolution or previous implementations.
- **No iteration history**: remove comments about previous decisions that are no longer relevant.
- **Focus on action/behavior**: comments describe current behavior and constraints, not change history.

### Docstring Standards (Public API)
- Document only public API (no leading underscore). Private members: one-line usage comment only.
- For functions/classes described in design docs, docstrings must include all information from the corresponding design section.
- Content: one-sentence summary; constraints/assumptions/side effects; parameters; return value; exceptions raised.
- No redundancy, no implementation details, no examples (examples go to docs/tests).
- Format: Google style.
  - Functions: summary, `Args:`, `Returns:`, `Raises:`.
  - Classes: summary, `Attributes:` (public only) + sections for constraints/assumptions/side effects.

## Type Safety
- Add type hints/annotations to all function parameters and return values.
- Prefer specific types over generic ones.
- **No Any**: do not use `Any`. Use concrete types. If unsure, query Context7/docs.

## Testing
- Prefer one assertion per test when practical.
- Use descriptive test names that state scenario and expectation.
- Follow Arrange–Act–Assert pattern.
- Keep tests focused and isolated; use fixtures for common setup.
- Cover positive and negative paths; assert error conditions explicitly.

## API Design
- Use core module APIs directly.
- Avoid direct dependencies on infrastructure services.
- Prefer exception-driven error handling.
- Build self-contained modules.
- Keep data containers passive; avoid embedding behavior in simple data models.
- Represent application logic as explicit callables/functions.

## Code Quality Workflow
### Pre-Modification Quality Check
- Run code quality tools on target files
- Check current score and identify issues
- Review and understand warnings before making changes

### During Development
- Follow control flow optimization guidelines
- Follow naming conventions and code structure rules
- Add appropriate type hints and documentation
- Use context managers for resource management
- Use appropriate design patterns

### Post-Modification Quality Check
- Run code quality tools again
- Target score: 9.0+ for all modules
- Fix all warnings before proceeding
- Apply code formatting tools
- Run import/organization tools
- Verify structure follows standards

### Phase Completion Quality Gate
- Run comprehensive code quality checks
- Check all files formatted consistently
- Run all unit tests
- Verify test coverage and quality
- Verify no critical issues remain
- All quality gates must pass before proceeding to next phase

## External Tool Integration
### Context7 Library Documentation
- Use Context7 to resolve library IDs and get documentation
- Get documentation for external libraries before integration
- Focus on specific topics relevant to current implementation

### DeepWiki Repository Exploration
- Use DeepWiki to explore repository structure
- Ask specific questions about implementation patterns
- Get repository structure before diving into code

### Documentation Policy
- **NEVER** create summary/README documents after task completion
- **NEVER** create TEST_UPDATE_GUIDE.md or similar summary files
- Update existing TODO files in place
- Keep documentation concise and integrated in existing structure
- Avoid redundant documentation that duplicates TODO content

## Language-Specific Guidelines
### General Principles
- Follow language-specific best practices
- Use appropriate design patterns for the language
- Maintain consistency with existing codebase style
- Use language-specific tools for quality assurance

## Code Organization
- Follow language-specific module/package organization
- Use appropriate import/export patterns
- Maintain clear separation of concerns
- Avoid circular dependencies
