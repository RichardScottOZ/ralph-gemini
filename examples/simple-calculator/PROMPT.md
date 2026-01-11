# PROMPT.md

## Task
Build a simple command-line calculator in Python that performs basic arithmetic operations.

Read clarify-session.md for full requirements.

## Instructions

1. Read TODO.md for current tasks
2. Pick the highest priority incomplete task
3. Read any files before editing them
4. Implement the task completely
5. Run tests with `pytest test_calculator.py`
6. If tests fail, fix before continuing
7. Mark the task complete in TODO.md by changing `[ ]` to `[x]`
8. Commit your changes with a clear message: `git add . && git commit -m "Task: [description]"`
9. Repeat steps 1-8 until all tasks are done

## Project Context

- **Language**: Python 3.11
- **Input**: Command line arguments (e.g., `python calculator.py 5 + 3`)
- **Output**: "Result: [number]" or "Error: [description]"
- **Operations**: +, -, *, /
- **Testing**: pytest

## Signs (Guardrails)

These are important rules to follow:

- **Keep it simple**: Use basic Python functions, no classes needed
- **Always read before editing**: Never edit a file without reading it first
- **Type hints**: Add type hints to all functions
- **Docstrings**: Include docstrings for all functions
- **PEP 8**: Follow PEP 8 style guide
- **Error handling**: Use try/except blocks for operations that might fail
- **Test before moving on**: Run `pytest test_calculator.py` after implementing features
- **Never skip failing tests**: Fix tests before moving to the next task
- **Clear error messages**: All errors start with "Error: "
- **Validate inputs**: Check that inputs are valid before processing
- **Keep commits focused**: Each commit should complete one logical task
- **Update TODO.md immediately**: Mark tasks done right after completing them

## Common Pitfalls to Avoid

- Don't implement operations beyond +, -, *, /
- Don't add a GUI or web interface
- Don't support chained operations (e.g., 1 + 2 + 3)
- Don't add advanced operations (sin, cos, log, etc.)
- Don't over-engineer - keep the solution simple

## Example Usage

After implementation, the calculator should work like this:

```bash
# Addition
python calculator.py 5 + 3
# Output: Result: 8

# Subtraction
python calculator.py 10 - 4
# Output: Result: 6

# Multiplication
python calculator.py 7 * 6
# Output: Result: 42

# Division
python calculator.py 20 / 4
# Output: Result: 5.0

# Division by zero
python calculator.py 10 / 0
# Output: Error: Division by zero

# Invalid operation
python calculator.py 5 % 3
# Output: Error: Invalid operation

# Non-numeric input
python calculator.py abc + 3
# Output: Error: Invalid number
```

## Testing Requirements

All tests must pass before marking tasks complete:

```bash
pytest test_calculator.py -v
```

Tests should cover:
- All four operations
- Integer and float inputs
- Division by zero
- Invalid operators
- Non-numeric inputs
- Edge cases (0, negatives, large numbers)

## Completion Criteria

When TODO.md shows all tasks are complete and all tests pass, output:

**DONE**

This signals the end of the execution loop.
