---
globs: **/design.md
alwaysApply: false
---
## [ClassName] Class

**Responsibility**: [Single sentence purpose]

**Properties**:
- `property: type` - Brief description
- `property: type` - Brief description

**[method_name(param: type) -> return_type]**
- **Behavior**: [What it does]
- **Input**: [Parameter description]
- **Output**: [Return description]
- **Raises**: [Exception conditions]

```python
# Example: minimal usage of method_name
result: return_type = instance.method_name(param)
```

---

## Exception Classes

**[ExceptionName]**: [When raised]

**[ExceptionName]**: [When raised]

---

## Validation Rules

**[Component] Validation**:
- [Validation rule]
- [Validation rule]

**[Component] Validation**:
- [Validation rule]
- [Validation rule]

---

## Design Change Policy

- Do not include legacy design details when design changes
- Do not consider backward compatibility
- All designs can be rebuilt from scratch
- No existing service compatibility requirements

## Design Modification Restrictions

- Never modify existing design without explicit user authorization
- Preserve original design intent and structure
- Do not change return types, parameter signatures, or method behaviors without user request
- Do not add, remove, or rename methods unless explicitly instructed
- Maintain exact API compatibility unless user specifically requests changes

---
```
</content>
</xai:function_call->