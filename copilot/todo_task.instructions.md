---
globs: **/todo.md
alwaysApply: false
---
## Task Organization

### Task States
- `[ ]` pending
- `[x]` completed

### Task Description Format
- Use action verb + object + detail
- Specify return type for methods
- Specify expected behavior for operations

### Task Scope
- Each task must be completable in single development session
- Include all required implementation details
- Specify all dependencies and prerequisites

### Design Compliance
- TODO documents must only contain implementation tasks for existing design
- No new design content allowed in TODO files
- All tasks must reference only APIs explicitly defined in design documents
- No speculation or creation of new interfaces in TODO content


---

## Code Quality Requirements

### Post-Implementation Checks
1. Run pylint on modified files
2. Run black formatter on modified files
3. Run isort import sorter on modified files
4. Fix all errors and warnings above threshold

### Quality Gates
- Pylint score ≥ 9.5 for all modified files
- Black formatting applied to all modified files
- Import sorting applied to all modified files
- No linting errors remain

---

## Testing Requirements

### Unit Test Coverage
- Create at least one unit test for each public method
- Create at least one unit test for each public function
- Test normal operation scenarios
- Test error conditions
- Test edge cases

### Test Structure
- Use Arrange-Act-Assert pattern
- Use descriptive test names: function_condition_expected
- Test one behavior per test method
- Use fixtures for common test data
- Mock external dependencies

---

## File Organization

### TODO File Structure
- One file per development phase
- Sequential numbering: 1.todo.md, 2.todo.md, etc.
- Each file contains related tasks only
- Split large phases across multiple files when needed

### Task Dependencies
- List prerequisite tasks explicitly
- Specify execution order when required
- Mark blocking dependencies clearly

---

## Status Management

### Progress Tracking
- Update task status immediately after completion
- Mark dependent tasks when prerequisites complete
- Use clear status indicators only

### Completion Criteria
- All tasks marked as completed
- All code passes quality gates
- All tests pass
- No blocking dependencies remain
