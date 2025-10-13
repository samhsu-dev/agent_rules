# Agent Rules

Predefined rules for AI-assisted development with Cursor and GitHub Copilot. Provides coding standards, documentation templates, and development workflows.

## Structure

```
agent_rules/
├── cursor/                    # Cursor rules (.mdc files)
│   ├── approach.instructions.mdc      # IDEA documentation
│   ├── codequality.instructions.mdc   # Code quality
│   ├── debugging.instructions.mdc     # Debugging
│   ├── requirements.instructions.mdc  # Design documentation
│   ├── testing.instructions.mdc       # Testing
│   └── todotasks.instructions.mdc    # Task management
├── copilot/                   # GitHub Copilot rules (.md files)
│   ├── approach.instructions.md      # IDEA documentation
│   ├── codequality.instructions.md   # Code quality
│   ├── debugging.instructions.md     # Debugging
│   ├── requirements.instructions.md  # Design documentation
│   ├── testing.instructions.md      # Testing
│   └── todotasks.instructions.md    # Task management
├── LICENSE
└── README.md
```

## Usage

### Cursor
```bash
cp cursor/*.mdc /path/to/project/.cursor/rules/
```

Reference in `.cursor/rules`:
```markdown
@codequality.instructions.mdc
@testing.instructions.mdc
```

### GitHub Copilot
```bash
mkdir -p .github
cp copilot/codequality.instructions.md .github/copilot-instructions.md
```

## Rules

| File | Purpose | Applies To |
|------|---------|------------|
| `requirements.instructions` | API/class documentation templates, SOLID principles | `**/design.md` |
| `codequality.instructions` | Coding standards, workflows, quality gates | All code files |
| `testing.instructions` | Testing guidelines, 5 layout profiles, mocking | Test files |
| `debugging.instructions` | Error handling, logging, recovery patterns | Error scenarios |
| `todotasks.instructions` | TODO templates, task management | `**/todo.md` |
| `approach.instructions` | Conceptual documentation, module boundaries | `**/idea.md` |

## Key Features

- **Design**: Class templates, exception patterns, modification restrictions
- **Code Quality**: Control flow optimization, error handling, performance guidelines
- **Testing**: Layout profiles A-E, unit/integration, mocking strategies, coverage ≥90%
- **Debugging**: Exception patterns, logging strategies, error recovery
- **Tasks**: State management, quality gates, templates for features/bugs/refactoring
- **IDEA**: Concept definitions, system roles, workflows, scenarios

## Customization

1. Copy relevant rule file to project
2. Modify for project-specific needs
3. Test with AI assistant
4. Iterate based on results

## Examples

**Python project**:
```markdown
# .cursor/rules
@codequality.instructions.mdc
@testing.instructions.mdc
- Use type hints for all functions
- Follow PEP 8
- Use pytest
```

**JavaScript project**:
```markdown
# .github/copilot-instructions.md
- Use Jest for testing
- Follow ESLint
- Use Prettier
```

## Contributing

Feel free to fork repository 

## License

MIT License - see [LICENSE](LICENSE)
