# Discovery Session - Simple Calculator

Started: 2024-01-10

## Project Overview

A simple command-line calculator application in Python that performs basic arithmetic operations.

## Questions Asked

### Core Requirements

1. **What is the main purpose of this project?**
   - Answer: Create a CLI calculator for basic arithmetic operations

2. **What is the MVP (Minimum Viable Product)?**
   - Answer: Calculator that accepts two numbers and an operator via command line, returns result

3. **What is explicitly out of scope?**
   - Answer: GUI, advanced operations (trigonometry, logarithms), expression parsing, chained operations

### Users & Context

4. **Who will use this?**
   - Answer: Developers and students learning Python

5. **What is their skill level?**
   - Answer: Basic to intermediate

### Technical Choices

6. **What programming language?**
   - Answer: Python 3.11

7. **What framework or libraries?**
   - Answer: Standard library only, pytest for testing

8. **What operations should be supported?**
   - Answer: Addition (+), Subtraction (-), Multiplication (*), Division (/)

9. **How should users input the operation?**
   - Answer: Command line arguments: `python calculator.py 5 + 3`

10. **What should the output format be?**
    - Answer: Simple text: "Result: 8"

### Integration Points

11. **Does this integrate with other systems?**
    - Answer: No, standalone CLI tool

12. **Any file I/O needed?**
    - Answer: No, just command line input/output

### Edge Cases & Error Handling

13. **What happens when dividing by zero?**
    - Answer: Print error message: "Error: Division by zero"

14. **What about invalid operations?**
    - Answer: Print error message: "Error: Invalid operation"

15. **What if non-numeric input is provided?**
    - Answer: Print error message: "Error: Invalid number"

16. **Should it support floating point numbers?**
    - Answer: Yes, both integers and floats

17. **What about very large numbers?**
    - Answer: Use Python's native number handling (no special limits for MVP)

### Quality Attributes

18. **What are the performance requirements?**
    - Answer: Must complete in < 1 second (trivial for simple arithmetic)

19. **What are the security considerations?**
    - Answer: Basic input validation to prevent crashes

20. **Should it have logging?**
    - Answer: No logging needed for this simple project

21. **What about tests?**
    - Answer: Yes, use pytest with tests for all operations and edge cases

### Existing Patterns

22. **Are there coding conventions to follow?**
    - Answer: Follow PEP 8, use type hints, include docstrings

23. **Any project structure preferences?**
    - Answer: Simple flat structure: calculator.py, test_calculator.py, README.md

### Preferences

24. **Any strong opinions on approach?**
    - Answer: Keep it simple, functional approach (no need for classes)

25. **Should the code be extensible?**
    - Answer: Not necessary for MVP, but keep it clean

26. **Any specific error messages format?**
    - Answer: Start with "Error: " followed by description

## Emerging Requirements

Based on the answers above, here are the key requirements:

### Functional Requirements
- Accept two numbers and an operator as command line arguments
- Support operations: +, -, *, /
- Return calculated result
- Handle both integers and floating point numbers
- Validate numeric inputs
- Validate operator
- Handle division by zero gracefully

### Non-Functional Requirements
- Complete calculation in < 1 second
- Clear error messages for all error cases
- Follow PEP 8 style guide
- Include type hints
- Include docstrings for functions
- Comprehensive pytest tests

### Testing Requirements
- Test all four operations
- Test with integers and floats
- Test division by zero
- Test invalid operator
- Test non-numeric input
- Test edge cases (0, negative numbers, very large numbers)

### Output Format
- Success: "Result: [number]"
- Error: "Error: [description]"

## Technical Decisions

- **Language**: Python 3.11
- **Input Method**: Command line arguments (sys.argv)
- **Testing**: pytest
- **Code Style**: PEP 8 with type hints
- **Structure**: Functional approach, no classes needed
- **Error Handling**: Try/except with clear messages

## File Structure

```
calculator/
├── calculator.py          # Main calculator logic and CLI
├── test_calculator.py     # pytest test suite
├── README.md             # Usage documentation
└── requirements.txt      # Dependencies (just pytest)
```

## Next Steps

1. Create PROMPT.md with execution instructions and guardrails
2. Create TODO.md with prioritized tasks and HARD STOP checkpoints
3. Run the execution loop with ralph-execute.sh
