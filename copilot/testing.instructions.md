---
description: apply only when modifying any files about testing
alwaysApply: false
---
# Testing Standards

## Test Organization
- Place tests under `tests/` with clear, predictable structure.
- Keep unit tests in `tests/unit/`; mirror source layout by module/component.
- Name files `test_<component>.py`; group closely related cases in `Test<ComponentName>`.
- Each test should assert one specific behavior.

## Test Structure
- Follow Arrange-Act-Assert pattern
- Use descriptive test method names: `test_<component>_<condition>_<expected>`
- Keep tests focused and isolated
- Use fixtures for common setup and teardown
- Avoid test interdependencies

```python
def test_parse_config_missing_file_raises():
    # Arrange
    path = "/does/not/exist.json"
    # Act & Assert
    with pytest.raises(FileNotFoundError):
        parse_config(path)
```

## Test Categories

### Unit Tests
- Fast; isolated from external systems; focused on a single unit.
- Live under `tests/unit/<module>/test_<component>.py`.

### Integration Tests (optional)
- Validate interaction across modules or with controlled external services.
- Use lightweight fakes/mocks; run separately from unit tests when possible.

## Test Naming Conventions
- Test classes: `Test<ComponentName>`
- Test methods: `test_<component>_<condition>_<expected>`
- Fixtures: `<component>_<state>()` (e.g., `sample_model()`, `empty_model()`)

```python
class TestUserRepository:
    def test_get_by_id_returns_none_when_absent(self, empty_repo):
        assert empty_repo.get_by_id("missing") is None
```

## Test Data Management
- Use fixtures for common test data
- Create specific fixtures for different scenarios
- Use temporary files for file operations
- Clean up resources automatically

```python
@pytest.fixture()
def temp_json(tmp_path: Path) -> Path:
    path = tmp_path / "sample.json"
    path.write_text("{}", encoding="utf-8")
    return path
```

## Assertion Guidelines
- One assertion per test when possible
- Use specific assertion methods
- Test both positive and negative cases
- Verify error conditions explicitly

```python
def test_sum_returns_total():
    assert add(2, 3) == 5
```

## Test Documentation
- Write clear test descriptions
- Explain complex test scenarios
- Document test data requirements
- Keep test code readable and maintainable

## Format
- Use pytest as the testing framework
- Follow Python naming conventions
- Use type hints in test code
- Import test dependencies clearly

```python
def test_normalize_amount_usd_value_is_identity() -> None:
    result = normalize_amount(10.0, "USD")
    assert result == 10.0
```

## Test Configuration

### pytest Configuration
- Use `conftest.py` for common fixtures
- Configure test discovery in `pyproject.toml`
- Use markers for test categorization
- Enable strict mode for better error reporting

### Test Running
- Use `pytest` to run tests
- Add `-v` for verbose output
- Add `-x` to stop on first failure
- Use `--tb=short` for concise tracebacks

### Test Coverage
- Aim for high test coverage (>90%)
- Focus on critical paths and edge cases
- Test error conditions and boundary values
- Verify exception handling

```bash
pytest --cov=src --cov-report=term-missing
```

## Test Maintenance

### Adding New Tests
1. Create test file in appropriate directory
2. Follow naming conventions
3. Use existing fixtures when possible
4. Write focused, isolated tests
5. Update documentation if needed

### Test Debugging
- Use descriptive test names
- Add debug prints when necessary
- Use pytest's `-s` flag to see print output
- Use `pytest.set_trace()` for debugging

### Test Performance
- Keep tests fast and focused
- Use mocks for external dependencies
- Avoid complex setup in test methods
- Use fixtures for expensive operations