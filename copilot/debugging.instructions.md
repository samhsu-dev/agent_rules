---
description: Only when any errors occurred during program execution
alwaysApply: false
---
# Internal Debugging

## Internal Debugging
- Use `__` prefixed functions for internal debugging only
- Import from `beluga_core.utils.debugging_log` directly
- Debug logs written to `.beluga/logs/debug.log`
- Not exposed in public API

## Exception Handling
- Use specific exception classes per stage
- Preserve original exception context with `from e`
- Catch exceptions at appropriate abstraction level
- Provide meaningful error messages

## API Error Patterns
- ModelingError: Model creation/validation errors
- BindingError: Code binding errors
- FuzzingError: Test execution errors
- ModelNotFoundError: File not found errors
- DuplicateIdError: ID conflict errors

## UI Error Handling
- Catch API exceptions in UI layer
- Display user-friendly error messages
- Use internal debugging for technical details
- Provide recovery options when possible

## Debugging Strategy
- Use exception traces to identify failure points
- Use internal debug logs for detailed flow tracking
- Check exception context for root causes
- Test error conditions explicitly
- Do not add internal debugging to serialization paths in beluga-core

## Format
- Use specific exception types
- Include context in error messages
- Preserve exception chains
- Handle exceptions gracefully
- Use internal debug functions with `__` prefix

## Examples

**Internal Debug Usage:**
```python
from beluga_core.utils.debugging_log import (
    __log_debug, __log_info, __log_error,
    __DebugContext, __log_api_call, __perf_monitor
)

# Basic debugging
__log_debug("Processing data", user_id="123")
__log_info("API call completed", service="modeling")

# Context debugging
with __DebugContext("data_processing", user_id="456"):
    # Process data
    pass

# Performance monitoring
__perf_monitor.start_timer("operation")
# ... do work ...
duration = __perf_monitor.end_timer("operation")
```

**API Exception Handling:**
```python
from beluga_core.modeling import ModelingService, ModelNotFoundError, DuplicateIdError

def load_model_safely(service, model_id):
    try:
        return service.load_model(model_id)
    except ModelNotFoundError as e:
        __log_error("Model not found", model_id=model_id, error=str(e))
        return None
    except DuplicateIdError as e:
        __log_error("ID conflict", model_id=model_id, error=str(e))
        raise
```

**UI Exception Handling:**
```python
class ModelingScreen(BaseScreen):
    def action_load_model(self):
        try:
            model = self.modeling_service.load_model("model.json")
            self.update_display(model)
        except ModelNotFoundError as e:
            self.show_error(f"Model not found: {e}")
        except Exception as e:
            self.show_error(f"Unexpected error: {e}")
```

**Exception Chaining:**
```python
def process_data(data):
    try:
        return validate_and_process(data)
    except ValidationError as e:
        raise ProcessingError("Data processing failed") from e
```

## Related Files
- `src/beluga_core/utils/debugging_log.py` (internal debugging utilities)
- `src/beluga_core/modeling/exceptions.py`
- `src/beluga_core/binding/exceptions.py`
- `src/beluga_core/fuzzing/exceptions.py`