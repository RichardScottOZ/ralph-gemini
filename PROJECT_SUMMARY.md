# Ralph Gemini - Project Summary

## Overview

**ralph-gemini** is an adaptation of the Ralph Wiggum autonomous development workflow for Google's Gemini CLI. It enables developers to automate repetitive coding tasks through an iterative AI-driven loop.

## What is Ralph Wiggum?

Ralph Wiggum is an autonomous development technique created by Geoffrey Huntley. The core concept is simple:

```bash
while :; do cat PROMPT.md | gemini -p "$(cat -)" ; done
```

A bash loop that repeatedly feeds instructions to an AI agent until a task is complete.

## Key Features

- **🎯 Autonomous Execution**: AI agent works independently through a task list
- **📋 3-Phase Workflow**: Clarify → Plan → Execute
- **🔁 Iterative Improvement**: Each failure teaches what guardrails to add
- **🛡️ Safety Features**: Max iterations, HARD STOP checkpoints, logging
- **📝 Context-Aware**: Uses GEMINI.md for project-specific context
- **🚀 Gemini 2.5 Pro**: 1M token context window with free tier access

## Architecture

```
┌─────────────────────────────────────────────────┐
│  Phase 1: CLARIFY (Interactive)                 │
│  ├─ User describes project                      │
│  ├─ Gemini asks 40-70 questions                 │
│  └─ Output: clarify-session.md                  │
└─────────────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────┐
│  Phase 2: PLAN (Interactive)                    │
│  ├─ Read clarify-session.md                     │
│  ├─ Generate PROMPT.md (instructions)           │
│  └─ Generate TODO.md (task checklist)           │
└─────────────────────────────────────────────────┘
                     ↓
┌─────────────────────────────────────────────────┐
│  Phase 3: EXECUTE (Autonomous Loop)             │
│  ├─ Loop: Read PROMPT.md                        │
│  ├─ Pick next task from TODO.md                 │
│  ├─ Implement task                              │
│  ├─ Run tests                                   │
│  ├─ Mark done in TODO.md                        │
│  ├─ Commit changes                              │
│  ├─ Repeat until "DONE"                         │
│  └─ Output: Working software                    │
└─────────────────────────────────────────────────┘
```

## Core Components

### 1. Templates
- **PROMPT.md**: Execution instructions with guardrails
- **TODO.md**: Prioritized task checklist with checkpoints
- **clarify-session.md**: Requirements from discovery phase
- **GEMINI.md**: Project context for Gemini CLI

### 2. Scripts
- **setup-ralph.sh**: Initialize new projects with Ralph workflow
- **ralph-execute.sh**: Run autonomous execution loop with safety features

### 3. Workflow Phases

#### Phase 1: Clarify
- Interactive Q&A session with Gemini
- 40-70 comprehensive questions
- Covers requirements, tech stack, constraints, edge cases
- Output: Structured requirements document

#### Phase 2: Plan
- Convert requirements to actionable tasks
- Generate execution instructions with guardrails
- Create prioritized task checklist
- Add HARD STOP verification points

#### Phase 3: Execute
- Autonomous loop until completion
- Each iteration: read prompt, pick task, implement, test, commit
- Git tracks progress
- Loop exits on "DONE" or max iterations

## Key Adaptations from ralph-kiro

| Aspect | ralph-kiro (Kiro CLI) | ralph-gemini (Gemini CLI) |
|--------|----------------------|--------------------------|
| **Agent Config** | `.kiro/agents/*.yaml` files | `GEMINI.md` context file |
| **Clarify** | `kiro-cli chat --agent ralph-clarify` | Interactive session with template |
| **Plan** | `kiro-cli chat --agent ralph-plan` | Interactive session with template |
| **Execute** | `kiro-cli chat --mode script` | `gemini -p "$(cat -)"` |
| **Context** | Agent YAML configs | GEMINI.md file |
| **Tools** | MCP servers | Built-in Google Search, shell, files |

## Philosophy

### The Playground Metaphor

> "Ralph is very good at making playgrounds, but he comes home bruised because he fell off the slide, so one then tunes Ralph by adding a sign next to the slide saying 'SLIDE DOWN, DON'T JUMP, LOOK AROUND,' and Ralph is more likely to look and see the sign."
>
> — Geoffrey Huntley

### Core Principles

1. **Deterministically Bad in an Undeterministic World**: Failures are predictable and informative
2. **Tune Prompts, Not Tools**: When Ralph fails, improve the instructions
3. **Eventual Consistency**: Trust that with enough guardrails, Ralph will succeed
4. **Signs as Guardrails**: Each failure teaches what signs to add

## Use Cases

### ✅ Good For
- Large refactoring projects
- Greenfield development with clear requirements
- Test-driven development loops
- Repetitive implementation tasks
- Boilerplate code generation
- API endpoint creation
- CRUD operations
- Configuration setup

### ❌ Not Ideal For
- Exploratory/research tasks
- Complex debugging of unknown issues
- Tasks requiring frequent human judgment
- High-stakes production changes without review
- Creative/design work
- Requirements gathering (use Phase 1 instead)

## Technical Requirements

- **Node.js**: 20 or higher
- **Gemini CLI**: Latest version
- **Git**: For state tracking
- **Bash**: For execution scripts
- **Authentication**: Google account, Gemini API key, or Vertex AI

## Installation

```bash
# Clone the repository
git clone https://github.com/RichardScottOZ/ralph-gemini.git
cd ralph-gemini

# Make scripts executable
chmod +x setup-ralph.sh ralph-execute.sh

# Install Gemini CLI
npm install -g @google/gemini-cli

# Authenticate
gemini
```

## Quick Example

```bash
# 1. Create project
./setup-ralph.sh my-api
cd my-api

# 2. Clarify requirements
gemini
> [Follow clarify template, save to clarify-session.md]

# 3. Generate execution files
gemini
> [Ask Gemini to create PROMPT.md and TODO.md]

# 4. Run autonomous loop
./ralph-execute.sh --max-iterations 30
```

## Monitoring and Tuning

### Monitoring
- Watch iteration output in real-time
- Check `ralph-execution.log` for full history
- Review git log for completed work
- Inspect TODO.md for progress

### Tuning
- Add guardrails to PROMPT.md based on failures
- Break down complex tasks in TODO.md
- Update GEMINI.md with project conventions
- Adjust max iterations based on project size

## Safety Features

1. **Max Iterations**: Prevents infinite loops
2. **HARD STOP Checkpoints**: Forces verification before continuing
3. **Logging**: Full execution history in log file
4. **Git Tracking**: Every change is committed
5. **Confirmation Prompt**: User must confirm before loop starts
6. **Rate Limiting**: Delays between iterations
7. **Error Detection**: Stops on STUCK signal

## Performance Characteristics

- **Free Tier**: 60 requests/min, 1,000 requests/day
- **Typical Project**: 10-50 iterations
- **Iteration Time**: 5-30 seconds per iteration
- **Total Time**: 15-30 minutes for small projects
- **Context Window**: 1M tokens (Gemini 2.5 Pro)

## Future Enhancements

- [ ] Support for custom commands
- [ ] Integration with CI/CD pipelines
- [ ] Multi-file context management
- [ ] Progress visualization
- [ ] Team collaboration features
- [ ] Checkpoint save/restore
- [ ] Parallel task execution

## Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## License

MIT License - Based on the original Ralph Wiggum workflow by Geoffrey Huntley, adapted from ralph-kiro by RichardScottOZ.

## Resources

- **Original Ralph Concept**: [https://ghuntley.com/ralph/](https://ghuntley.com/ralph/)
- **Gemini CLI**: [https://github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)
- **ralph-kiro**: [https://github.com/RichardScottOZ/ralph-kiro](https://github.com/RichardScottOZ/ralph-kiro)

---

**Version**: 1.0.0  
**Last Updated**: January 2026  
**Maintainer**: RichardScottOZ
