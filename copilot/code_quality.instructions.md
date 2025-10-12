---
description: use those rules if and only if related to codes and programming
alwaysApply: false
---
# Code Quality Standards

## Control Flow Optimization
- Prefer early returns over nested conditionals.
- Use guard clauses to minimize nesting and improve readability.
- Use `continue` to skip iterations instead of nested `if` blocks.
- Use `break` to exit loops when conditions are met.
- In singleton `__new__`, use early returns to keep logic flat.

```python
def process(data):
    if data is None or not data.is_valid():  # early return
        return None
    for item in data.items:
        if not item.enabled:
            continue  # skip instead of nesting
        if item.is_terminal:
            break
    return transform(data)
```

## Error Handling
- Catch specific exception types (avoid broad `except Exception`).
- Handle errors at the appropriate abstraction level.
- Preserve original exception context across call chains.

```python
def load_config(path: str) -> dict:
    try:
        with open(path, 'r', encoding='utf-8') as f:
            return json.load(f)
    except FileNotFoundError as exc:
        raise ConfigNotFoundError(path) from exc
    except json.JSONDecodeError as exc:
        raise InvalidConfigError(path) from exc
```

## Code Structure
- Keep functions short (ideally < 20 lines).
- Extract complex logic into dedicated functions.
- Avoid deep nesting (max 3 levels).

```python
def compute_score(user):
    if not is_eligible(user):
        return 0
    base = base_score(user)
    bonus = compute_bonus(user)
    return base + bonus
```

## Performance
- Use context managers for resource management/cleanup.
- Avoid unnecessary object creation in loops.
- Check caches before expensive operations.

```python
with db.connect() as conn:  # ensures cleanup
    rows = conn.fetch_all(query)
    for row in rows:
        process_row(row)  # reuse objects; avoid per-iter allocations
```

## Documentation
- Use English for comments and docs.
- Explain why (rationale) rather than what.
- Add type hints to all function parameters and return values.
- Prefer specific types over `Any`.

```python
def normalize_amount(amount: float, currency: str) -> float:
    """Converts amount to a canonical unit for comparison (ensures ordering is meaningful)."""
    rate = EXCHANGE_RATES[currency]
    return amount * rate
```

## Testing
- Prefer one assertion per test when practical.
- Use descriptive test names that state scenario and expectation.
- Follow Arrange–Act–Assert.
- Keep tests focused and isolated; use fixtures for common setup.
- Cover positive and negative paths; assert error conditions explicitly.

```python
def test_normalize_amount_usd_value_is_identity():
    # Arrange
    amount = 10.0
    # Act
    result = normalize_amount(amount, "USD")
    # Assert
    assert result == 10.0
```

## API Design
- Use core domain APIs directly.
- Avoid direct dependencies on infrastructure services.
- Prefer exception-driven error handling.
- Build self-contained modules.
- Keep data containers passive; avoid embedding behavior in simple data models.
- Represent business logic as explicit callables/functions; prefer no-closure lambdas or small, pure functions.

```python
@dataclass
class Order:
    id: str
    total: float

def is_large_order(order: Order) -> bool:  # logic lives outside the data class
    return order.total > 100.0
```

## Callable Serialization Policy
- Serialize callables without closures as: {"__callable__": "function", "name": "<lambda>", "code": base64(marshal(code))}.
- Deserialize via base64+marshal and `types.FunctionType`.
- Do not serialize closures (bytecode is version-specific).

```python
def serialize_function(fn):
    return {"__callable__": "function", "name": getattr(fn, "__name__", "<lambda>"), "code": base64.b64encode(marshal.dumps(fn.__code__)).decode()}
```

## __init__.py File Standards
- Follow a unified structure template for all `__init__.py` files.
- Include clear module documentation with usage examples.
- Group imports: standard library → third-party → local.
- Organize `__all__` by functional groups.
- Avoid circular imports and duplicate definitions.

```python
"""
[Module Name] module.

[Short description and functionality]

## Usage

···python
from package.module import ClassName, function_name
···
"""

# 1. Standard library imports
from typing import Dict, Any

# 2. Third-party imports

# 3. Local imports

__all__ = [
    "PublicClass",
    "public_function",
]
```

## Format
- Import order: standard library → third-party → local.
- Use type hints for all functions.
- Use context managers for resource management.
- Use reactive attributes and watchers for UI data binding.

## Pylint Policy
- **NEVER** use `# pylint: disable` comments to bypass checks
- Accept reasonable warnings (e.g., too-many-arguments for design-required methods)
- Focus on fixing actual code issues rather than suppressing warnings
- Only address critical issues that affect functionality or maintainability
- Target Pylint score 9.0+ without using disable comments

## Code Quality Workflow

### Pre-Modification Quality Check
- Run Pylint on target file: `pylint src/beluga_core/path/to/file.py`
- Check current score and identify issues
- Review and understand warnings before making changes

### During Development
- Follow control flow optimization guidelines
- Follow naming conventions and code structure rules
- Add appropriate type hints and documentation
- Use context managers for resource management
- Use SerializableMixin for data classes

### Post-Modification Quality Check
- Run Pylint again: `pylint src/beluga_core/path/to/file.py --score=y`
- Target score: 9.5+ for all modules
- Fix all warnings before proceeding
- Run Black formatting: `black src/beluga_core/path/to/file.py`
- Run import sorting: `isort src/beluga_core/path/to/file.py`
- For `__init__.py` files: verify structure follows standard template
- Check for circular imports and duplicate definitions
- Ensure `__all__` lists are complete and properly grouped

### Phase Completion Quality Gate
- Run comprehensive Pylint: `pylint src/beluga_core/ --score=y --reports=y`
- Check all files formatted: `black --check src/beluga_core/`
- Check import sorting: `isort --check-only src/beluga_core/`
- Run all unit tests: `uv run pytest tests/unit/ -v`
- Verify test coverage and quality
- Verify no critical issues remain
- Audit all `__init__.py` files for standard compliance
- Ensure no circular imports or duplicate definitions
- Verify all modules have proper documentation and `__all__` lists
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