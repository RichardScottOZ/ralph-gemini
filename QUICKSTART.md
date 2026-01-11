# 🚀 Ralph Wiggum Quick Start Guide

Get up and running with Ralph Wiggum for Gemini CLI in 5 minutes.

## Prerequisites

1. **Install Gemini CLI**

```bash
# Using npm (recommended)
npm install -g @google/gemini-cli

# Or with Homebrew
brew install gemini-cli

# Verify installation
gemini --version
```

2. **Authenticate**

```bash
# Start Gemini CLI
gemini

# Choose "Login with Google" when prompted
# Follow the browser authentication flow
```

## Setup Your First Project

### Step 1: Clone ralph-gemini

```bash
git clone https://github.com/RichardScottOZ/ralph-gemini.git
cd ralph-gemini
```

### Step 2: Create Your Project

```bash
# Use the setup script
./setup-ralph.sh my-project

# Navigate to your new project
cd my-project
```

Your project now has:
- `PROMPT.md` - Instructions for execution
- `TODO.md` - Task checklist
- `clarify-session.md` - Requirements template
- `GEMINI.md` - Project context
- `ralph-execute.sh` - Execution script

## The 3-Phase Workflow

### Phase 1: Clarify (Gather Requirements)

Start an interactive Gemini session to gather requirements:

```bash
gemini
```

In the chat, use this template:

```
I want to use the Ralph Wiggum technique to gather comprehensive requirements.
Please ask me 40-70 detailed questions about my project, covering:
- Core requirements and MVP
- Users and context
- Technical choices (language, framework, database)
- Integration points
- Edge cases and error handling
- Quality attributes (performance, security)
- Existing patterns and conventions
- Preferences and tradeoffs

My project is: [DESCRIBE YOUR PROJECT IN 1-2 SENTENCES]

After we complete all questions, help me save the results to clarify-session.md
```

**Example:**
```
My project is: A REST API for managing tasks, with user authentication and PostgreSQL storage.
```

Answer the questions thoroughly. This phase typically takes 15-30 minutes.

### Phase 2: Plan (Generate Execution Files)

Start another Gemini session to create execution files:

```bash
gemini
```

In the chat:

```
Please read clarify-session.md and create two files:

1. PROMPT.md - Execution instructions with:
   - Clear task descriptions
   - Step-by-step instructions
   - Guardrails to prevent common mistakes
   - Completion criteria ("output: DONE" when finished)

2. TODO.md - Prioritized task checklist with:
   - Critical tasks (Must Have)
   - Important tasks (Should Have)
   - Nice to have tasks
   - HARD STOP checkpoints for verification
   - Clear completion criteria for each task

Make sure the tasks are specific and actionable.
```

Gemini will create or update these files for you.

### Phase 3: Execute (Autonomous Loop)

Run the Ralph execution loop:

```bash
# Using the provided script (recommended)
./ralph-execute.sh --max-iterations 30

# Or manually
max_iterations=50
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

The loop will:
1. Read PROMPT.md
2. Pick the next task from TODO.md
3. Implement it
4. Mark it done
5. Commit changes
6. Repeat until DONE

## Real Example

Let's build a simple Python calculator:

### 1. Clarify

```bash
cd my-calculator
gemini
```

Answer Gemini's questions:
- **What operations?** Add, subtract, multiply, divide
- **CLI or GUI?** CLI only for MVP
- **Error handling?** Yes, handle division by zero
- **Testing?** Yes, use pytest
- **Language?** Python 3.11

Save to `clarify-session.md`

### 2. Plan

```bash
gemini
```

Ask Gemini to generate files. Your `TODO.md` might look like:

```markdown
# TODO

## Critical
- [ ] Create basic calculator module with operations
- [ ] Add CLI interface
- [ ] Add error handling for division by zero
- [ ] **HARD STOP** - Verify calculator works for all operations

## Important
- [ ] Add pytest tests
- [ ] Add input validation
- [ ] Create README

## Completed
```

### 3. Execute

```bash
./ralph-execute.sh --max-iterations 20
```

Watch Ralph work through the tasks!

## Tips for Success

### 1. Be Specific in Clarify Phase

❌ Bad: "Make it fast"  
✅ Good: "Must handle 100 requests/second under normal load"

### 2. Add Guardrails to PROMPT.md

```markdown
## Signs (Guardrails)
- Always read files before editing
- Never skip failing tests
- Don't refactor unrelated code
- Keep commits focused on one task
```

### 3. Use HARD STOP Checkpoints

```markdown
- [ ] Implement feature X
- [ ] **HARD STOP** - Verify feature X works before continuing
```

### 4. Start Small

For your first project:
- Keep it simple (< 500 lines of code)
- Use familiar tech stack
- Clear, well-defined requirements
- Short task list (10-15 tasks)

### 5. Monitor and Tune

If Ralph gets stuck:
1. Check the output - what went wrong?
2. Update PROMPT.md with more specific guardrails
3. Break down the current task in TODO.md
4. Resume execution

## Common Issues

### "gemini command not found"

```bash
# Install Gemini CLI
npm install -g @google/gemini-cli

# Or with npx (no installation)
npx @google/gemini-cli
```

### Loop runs forever

- Ensure PROMPT.md says "output: DONE" when complete
- Add `--max-iterations` limit
- Check TODO.md for remaining tasks

### Tasks not getting marked done

Add to PROMPT.md:
```markdown
7. Mark the task complete in TODO.md by changing [ ] to [x]
8. Update the TODO.md file immediately
```

### Rate limiting

```bash
# Add longer delay between iterations
sleep 5  # Instead of sleep 2
```

## Next Steps

1. **Read the full README.md** for detailed information
2. **Try a sample project** - start with something small
3. **Join the community** - share your results and learn from others
4. **Tune your prompts** - the more you use Ralph, the better it gets

## Resources

- **Main Documentation**: [README.md](README.md)
- **Ralph Philosophy**: [https://ghuntley.com/ralph/](https://ghuntley.com/ralph/)
- **Gemini CLI Docs**: [https://github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)
- **Original ralph-kiro**: [https://github.com/RichardScottOZ/ralph-kiro](https://github.com/RichardScottOZ/ralph-kiro)

---

**Happy autonomous coding! 🤖**
