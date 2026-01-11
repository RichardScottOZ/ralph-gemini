# Simple Calculator Example

This example demonstrates how to use Ralph Wiggum with Gemini CLI to build a simple command-line calculator in Python.

## Project Goal

Build a Python CLI calculator that can:
- Perform basic operations (add, subtract, multiply, divide)
- Handle errors (division by zero, invalid input)
- Include unit tests with pytest

## Phase 1: Clarify Session

Here's what a clarify session might look like:

### Questions & Answers

**Q: What programming language?**
A: Python 3.11

**Q: What operations should the calculator support?**
A: Addition, subtraction, multiplication, and division

**Q: CLI or GUI?**
A: CLI only for MVP

**Q: How should users input operations?**
A: Command line arguments: `python calculator.py 5 + 3`

**Q: What error handling is needed?**
A: Handle division by zero and invalid operations

**Q: Should it support floating point numbers?**
A: Yes, both integers and floats

**Q: What testing framework?**
A: pytest

**Q: Any special output formatting?**
A: Just print the result, e.g., "Result: 8"

**Q: Should it support chained operations?**
A: No, just two operands for MVP

**Q: Any logging requirements?**
A: No logging needed for this simple project

See [clarify-session.md](clarify-session.md) for the full discovery session.

## Phase 2: Plan

The plan phase generates two files:

### PROMPT.md

Contains execution instructions and guardrails. See [PROMPT.md](PROMPT.md).

### TODO.md

Contains prioritized task list. See [TODO.md](TODO.md).

## Phase 3: Execute

Run the execution loop:

```bash
# Using the ralph-execute.sh script
../../ralph-execute.sh --max-iterations 20

# Or manually
max_iterations=20
iteration=0

while [ $iteration -lt $max_iterations ]; do
  echo "Iteration $((iteration + 1))/$max_iterations"
  output=$(cat PROMPT.md | gemini -p "$(cat -)")
  echo "$output"
  
  if echo "$output" | grep -q "DONE"; then
    echo "Task completed!"
    break
  fi
  
  iteration=$((iteration + 1))
  sleep 2
done
```

## Expected Output

After Ralph completes:

```
calculator/
├── calculator.py          # Main calculator module
├── test_calculator.py     # pytest tests
├── README.md             # Project documentation
└── requirements.txt      # Python dependencies (pytest)
```

## Running the Calculator

```bash
# Install dependencies
pip install -r requirements.txt

# Run tests
pytest test_calculator.py

# Use the calculator
python calculator.py 5 + 3
# Result: 8

python calculator.py 10 / 2
# Result: 5.0

python calculator.py 10 / 0
# Error: Division by zero
```

## Key Learnings

This simple example demonstrates:

1. **Clear Requirements**: Simple, well-defined scope makes Ralph very effective
2. **Test-Driven**: Having tests ensures quality
3. **Error Handling**: Guardrails prompt Ralph to handle edge cases
4. **Iterative**: Ralph works through tasks one at a time
5. **Git History**: Each task completion is a commit

## Iteration Breakdown

Typical execution for this project:

1. **Iteration 1**: Create calculator.py with basic structure
2. **Iteration 2**: Implement addition and subtraction
3. **Iteration 3**: Implement multiplication and division
4. **Iteration 4**: Add error handling for division by zero
5. **Iteration 5**: Create test_calculator.py with basic tests
6. **Iteration 6**: Add tests for all operations
7. **Iteration 7**: Add tests for error cases
8. **Iteration 8**: Run tests, fix any failures
9. **Iteration 9**: Create README.md
10. **Iteration 10**: Create requirements.txt
11. **Iteration 11**: Mark all tasks done, output DONE

Total iterations: ~11
Total time: ~5-10 minutes

## Tips for This Example

1. **Start Simple**: This is a great first Ralph project
2. **Clear Input**: Command line args are easy to test
3. **Good Error Handling**: Division by zero is a clear edge case
4. **Testable**: Unit tests verify each operation
5. **Fast Iterations**: Simple tasks complete quickly

## Try It Yourself

```bash
# From ralph-gemini root directory
cd examples
mkdir my-calculator
cd my-calculator

# Copy this example's files as starting point
cp ../simple-calculator/clarify-session.md .
cp ../simple-calculator/PROMPT.md .
cp ../simple-calculator/TODO.md .
cp ../simple-calculator/GEMINI.md .

# Run the execution loop
../../ralph-execute.sh --max-iterations 15
```

## Common Issues

### Issue: Ralph creates complex code

**Solution**: Add guardrail to PROMPT.md:
```markdown
Keep the code simple. Use basic Python functions, no classes needed for this simple project.
```

### Issue: Tests don't cover edge cases

**Solution**: Add to TODO.md:
```markdown
- [ ] Add test for division by zero
- [ ] Add test for invalid operation
- [ ] Add test for non-numeric input
```

### Issue: Ralph skips error handling

**Solution**: Add to PROMPT.md:
```markdown
Always implement error handling. Use try/except blocks for operations that might fail.
```

## Next Steps

After mastering this example:
1. Try the [REST API example](../rest-api/)
2. Build your own simple project
3. Experiment with different prompts and guardrails
4. Share your results with the community

---

**Difficulty**: Beginner  
**Estimated Time**: 15-20 minutes  
**Lines of Code**: ~50-100
