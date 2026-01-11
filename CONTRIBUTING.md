# Contributing to ralph-gemini

Thank you for your interest in contributing to ralph-gemini! This document provides guidelines for contributing to the project.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [How Can I Contribute?](#how-can-i-contribute)
- [Development Setup](#development-setup)
- [Submitting Changes](#submitting-changes)
- [Style Guidelines](#style-guidelines)
- [Testing](#testing)

## Code of Conduct

This project and everyone participating in it is governed by basic principles of respect and professionalism. By participating, you are expected to uphold this code.

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check existing issues to avoid duplicates. When creating a bug report, include:

- **Clear title and description**
- **Steps to reproduce** the issue
- **Expected behavior** vs actual behavior
- **Environment details** (OS, Gemini CLI version, Node.js version)
- **Logs** from `ralph-execution.log` if applicable

### Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues. When creating an enhancement suggestion, include:

- **Clear use case** for the enhancement
- **Proposed solution** or approach
- **Alternatives considered**
- **Examples** of how it would work

### Pull Requests

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Test your changes thoroughly
5. Commit with clear messages (`git commit -m 'Add amazing feature'`)
6. Push to your fork (`git push origin feature/amazing-feature`)
7. Open a Pull Request

## Development Setup

### Prerequisites

- Bash 4.0 or higher
- Git
- Node.js 20 or higher
- Gemini CLI installed

### Local Setup

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/ralph-gemini.git
cd ralph-gemini

# Make scripts executable
chmod +x setup-ralph.sh ralph-execute.sh

# Test the setup script
./setup-ralph.sh test-project
cd test-project

# Verify structure
ls -la
```

## Submitting Changes

### Commit Messages

Use clear, descriptive commit messages:

```
Add support for custom completion words

- Allow users to specify custom completion word via --completion-word
- Update documentation with examples
- Add validation for completion word parameter
```

Format:
- First line: Summary (50 chars or less)
- Blank line
- Detailed description with bullets for multiple changes

### Pull Request Guidelines

- **One feature per PR**: Keep PRs focused on a single enhancement or fix
- **Update documentation**: Include relevant doc updates
- **Test your changes**: Verify scripts work as expected
- **Update CHANGELOG**: Add entry for your change
- **Reference issues**: Link related issues in PR description

Example PR description:

```markdown
## Description
Adds support for custom completion words in ralph-execute.sh

## Changes
- Added --completion-word parameter to ralph-execute.sh
- Updated help text and documentation
- Added validation for the parameter

## Testing
Tested with completion words: DONE, COMPLETE, FINISHED

## Related Issues
Closes #123
```

## Style Guidelines

### Shell Scripts

- Use `#!/bin/bash` shebang
- Enable strict mode: `set -e`
- Use meaningful variable names in UPPER_CASE
- Add comments for complex logic
- Use functions for reusable code
- Include help text (`--help` flag)

Example:

```bash
#!/bin/bash
set -e

# Configuration
MAX_ITERATIONS=50
LOG_FILE="ralph-execution.log"

# Display help message
show_help() {
    echo "Usage: $0 [OPTIONS]"
    echo ""
    echo "Options:"
    echo "  --max-iterations N    Maximum iterations"
    echo "  --help               Show this help"
}

# Main function
main() {
    # Parse arguments
    while [[ $# -gt 0 ]]; do
        case $1 in
            --help)
                show_help
                exit 0
                ;;
            *)
                echo "Unknown option: $1"
                exit 1
                ;;
        esac
    done
}

main "$@"
```

### Markdown Documentation

- Use ATX-style headers (`#` not `===`)
- Include table of contents for long documents
- Use code blocks with language tags
- Include examples for all features
- Keep lines under 100 characters when possible
- Use lists for steps or options

### Templates

- Keep templates simple and general-purpose
- Include comments explaining each section
- Provide examples where helpful
- Use clear, descriptive placeholders like `[DESCRIPTION]`

## Testing

### Testing Scripts

Before submitting, test your changes:

```bash
# Test setup script
./setup-ralph.sh test-project-1
cd test-project-1
# Verify all files are created
ls -la
# Check file contents
cat PROMPT.md
cd ..

# Test with different project names
./setup-ralph.sh test-project-2
cd test-project-2

# Clean up
cd ..
rm -rf test-project-1 test-project-2
```

### Testing Execution Loop

```bash
# Create a minimal test project
./setup-ralph.sh test-exec
cd test-exec

# Create a simple PROMPT.md
cat > PROMPT.md << 'EOF'
Create a file called test.txt with the word "SUCCESS" in it.
When done, output: DONE
EOF

# Test execution (with low max iterations)
../ralph-execute.sh --max-iterations 5

# Verify
cat test.txt  # Should contain "SUCCESS"
```

### Manual Testing Checklist

Before submitting a PR, verify:

- [ ] `setup-ralph.sh --help` displays help text
- [ ] `setup-ralph.sh my-project` creates all expected files
- [ ] All template files are copied correctly
- [ ] Scripts have execute permissions
- [ ] `ralph-execute.sh --help` displays help text
- [ ] `ralph-execute.sh` validates PROMPT.md exists
- [ ] `ralph-execute.sh` checks for gemini CLI
- [ ] Loop exits on completion word
- [ ] Loop exits on max iterations
- [ ] Log file is created with proper content
- [ ] Documentation is up to date

## Project Structure

```
ralph-gemini/
├── README.md              # Main documentation
├── QUICKSTART.md          # Quick start guide
├── PROJECT_SUMMARY.md     # Project overview
├── CONTRIBUTING.md        # This file
├── LICENSE               # MIT License
├── setup-ralph.sh        # Project setup script
├── ralph-execute.sh      # Execution loop script
├── templates/            # Template files
│   ├── PROMPT.md
│   ├── TODO.md
│   ├── clarify-session.md
│   └── GEMINI.md
└── examples/             # Example projects
    ├── simple-calculator/
    └── rest-api/
```

## Areas for Contribution

### High Priority
- Additional examples in `examples/`
- Improved error handling in scripts
- Windows compatibility (PowerShell versions)
- Integration tests

### Medium Priority
- Additional templates for common project types
- Improved logging and progress tracking
- Configuration file support
- Checkpoint save/restore

### Documentation
- Video tutorials
- More detailed examples
- Troubleshooting guide expansion
- Translation to other languages

## Questions?

Feel free to open an issue with the `question` label if you have any questions about contributing.

## Recognition

Contributors will be recognized in:
- GitHub contributors list
- Release notes for their contributions
- README acknowledgments section (for significant contributions)

Thank you for contributing to ralph-gemini! 🎉
