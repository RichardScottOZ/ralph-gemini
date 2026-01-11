# Project Context for Gemini CLI

## Project Overview

Simple command-line calculator in Python for basic arithmetic operations.

## Tech Stack

- **Language**: Python 3.11
- **Framework**: None (standard library)
- **Testing**: pytest
- **Build Tool**: pip

## Build & Test Commands

```bash
# Install dependencies
pip install -r requirements.txt

# Run tests
pytest test_calculator.py

# Run tests with verbose output
pytest test_calculator.py -v

# Run the calculator
python calculator.py 5 + 3
```

## Project Structure

```
calculator/
├── calculator.py          # Main calculator logic and CLI interface
├── test_calculator.py     # pytest test suite
├── README.md             # Usage documentation
└── requirements.txt      # Python dependencies
```

## Coding Conventions

- **Style**: Follow PEP 8 style guide
- **Type Hints**: Add type hints to all function signatures
- **Docstrings**: Include docstrings for all functions
- **Naming**: Use snake_case for functions and variables
- **Error Messages**: Start all error messages with "Error: "
- **Simplicity**: Use functional approach, no classes needed

## Important Context

- Input via command line arguments: `python calculator.py [num1] [operator] [num2]`
- Operations: +, -, *, / only
- Support both integers and floats
- Output format: "Result: [number]" for success, "Error: [description]" for errors
- All edge cases must be handled: division by zero, invalid operators, non-numeric input

## Common Pitfalls to Avoid

- Don't implement operations beyond +, -, *, /
- Don't add GUI or web interface
- Don't support chained operations
- Don't add logging (not needed for this simple project)
- Don't over-engineer - keep it simple

## Testing Requirements

- Use pytest for all tests
- Test all four operations
- Test error cases (division by zero, invalid operator, invalid number)
- Test edge cases (0, negatives, floats, large numbers)
- All tests must pass before marking task complete

## Example Output

```bash
# Success cases
python calculator.py 5 + 3    # Output: Result: 8
python calculator.py 10 - 4   # Output: Result: 6
python calculator.py 7 * 6    # Output: Result: 42
python calculator.py 20 / 4   # Output: Result: 5.0

# Error cases
python calculator.py 10 / 0   # Output: Error: Division by zero
python calculator.py 5 % 3    # Output: Error: Invalid operation
python calculator.py abc + 3  # Output: Error: Invalid number
```
