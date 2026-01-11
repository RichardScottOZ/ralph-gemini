# Verification Guide for ralph-gemini

This guide helps you verify that ralph-gemini is working correctly.

## Pre-Verification Checklist

Before testing ralph-gemini, ensure you have:

- [ ] Node.js 20 or higher installed
- [ ] Gemini CLI installed (`npm install -g @google/gemini-cli` or `brew install gemini-cli`)
- [ ] Git installed
- [ ] Bash shell available
- [ ] Authenticated with Gemini CLI (run `gemini` and login)

## Verification Steps

### 1. Verify Installation

```bash
# Check Gemini CLI is installed
gemini --version
# Should output version number like: 1.x.x

# Check Node.js version
node --version
# Should be v20.x.x or higher

# Check Git
git --version
# Should be 2.x.x or higher
```

### 2. Test Setup Script

```bash
# Clone the repository
git clone https://github.com/RichardScottOZ/ralph-gemini.git
cd ralph-gemini

# Verify scripts are executable
ls -la *.sh
# Should show rwxr-xr-x permissions

# Test help flag
./setup-ralph.sh --help
# Should display help text

# Create a test project
./setup-ralph.sh test-verify
cd test-verify

# Verify all files were created
ls -la
# Should show: PROMPT.md, TODO.md, clarify-session.md, GEMINI.md, ralph-execute.sh, README.md, .gitignore, src/

# Verify git repository was initialized
git log
# Should show initial commit

# Clean up
cd ..
rm -rf test-verify
```

### 3. Test Execute Script

```bash
# Create a minimal test project
./setup-ralph.sh test-exec
cd test-exec

# Create a minimal PROMPT.md for testing
cat > PROMPT.md << 'EOF'
# Test Prompt

Create a file called SUCCESS.txt with the text "Test completed successfully!"

After creating the file, output: DONE
EOF

# Verify ralph-execute.sh help
./ralph-execute.sh --help
# Should display help text

# Note: Actually running the execution loop requires Gemini CLI to be properly authenticated
# and may consume API quota, so we won't run it in verification
echo "Execution script structure verified"

# Clean up
cd ..
rm -rf test-exec
```

### 4. Verify Templates

```bash
cd ralph-gemini

# Check all template files exist
ls -la templates/
# Should show: GEMINI.md, PROMPT.md, TODO.md, clarify-session.md

# Verify template contents are not empty
wc -l templates/*
# All files should have content

# Check template structure
head -5 templates/PROMPT.md
# Should show "# PROMPT.md" header
```

### 5. Verify Example

```bash
cd ralph-gemini

# Check example exists
ls -la examples/simple-calculator/
# Should show: README.md, PROMPT.md, TODO.md, clarify-session.md, GEMINI.md

# Verify example is well-documented
cat examples/simple-calculator/README.md | head -20
# Should show clear documentation
```

### 6. Verify Documentation

```bash
cd ralph-gemini

# Check all documentation files exist
ls -la *.md
# Should show: README.md, QUICKSTART.md, PROJECT_SUMMARY.md, CONTRIBUTING.md

# Verify README has content
wc -l README.md
# Should be substantial (500+ lines)

# Check for broken internal links (simple check)
grep -n "](.*\.md)" README.md
# Manually verify these links point to existing files
```

## Functional Testing (Optional)

If you want to test the full workflow with actual Gemini CLI:

### Simple Test Project

```bash
# 1. Create a test project
./setup-ralph.sh calculator-test
cd calculator-test

# 2. Manually create a simple clarify-session.md
cat > clarify-session.md << 'EOF'
# Simple Test Project

## Requirements
- Create a Python script that prints "Hello, Ralph!"
- Save it as hello.py
- No other requirements

## Technical Decisions
- Python 3.x
- No external dependencies
- Simple print statement
EOF

# 3. Create PROMPT.md
cat > PROMPT.md << 'EOF'
# PROMPT.md

## Task
Create a Python script that prints "Hello, Ralph!"

## Instructions
1. Create hello.py with a print statement
2. Update TODO.md to mark task complete
3. Commit the file
4. Output: DONE

## Completion
When hello.py exists and TODO.md is updated, output: DONE
EOF

# 4. Update TODO.md
cat > TODO.md << 'EOF'
# TODO

## Tasks
- [ ] Create hello.py that prints "Hello, Ralph!"

## Completed
EOF

# 5. Run execution loop (only if authenticated with Gemini CLI)
# ./ralph-execute.sh --max-iterations 5

# 6. Manually test (without running loop)
echo "print('Hello, Ralph!')" > hello.py
python hello.py
# Should output: Hello, Ralph!

# Clean up
cd ..
rm -rf calculator-test
```

## Verification Checklist

After completing the steps above, verify:

### Repository Structure
- [ ] All core files present (README, QUICKSTART, etc.)
- [ ] Scripts are executable (setup-ralph.sh, ralph-execute.sh)
- [ ] Templates directory exists with all templates
- [ ] Examples directory exists with at least one example
- [ ] LICENSE file exists
- [ ] .gitignore is present

### Scripts Functionality
- [ ] setup-ralph.sh --help works
- [ ] setup-ralph.sh creates project with all files
- [ ] Created projects have proper git initialization
- [ ] ralph-execute.sh --help works
- [ ] ralph-execute.sh has proper permissions
- [ ] Both scripts handle errors gracefully

### Documentation Quality
- [ ] README is comprehensive and clear
- [ ] QUICKSTART provides easy entry point
- [ ] PROJECT_SUMMARY explains architecture
- [ ] CONTRIBUTING has clear guidelines
- [ ] Example documentation is complete
- [ ] All markdown files are well-formatted

### Templates
- [ ] All template files have clear placeholders
- [ ] Templates follow consistent structure
- [ ] GEMINI.md template is useful
- [ ] PROMPT.md has good guardrails example
- [ ] TODO.md shows proper format

### Examples
- [ ] simple-calculator example is complete
- [ ] Example has all required files
- [ ] Example documentation is clear
- [ ] Example demonstrates full workflow

## Common Issues

### Issue: "gemini: command not found"

**Solution:**
```bash
# Install Gemini CLI
npm install -g @google/gemini-cli

# Verify installation
gemini --version
```

### Issue: "Permission denied" when running scripts

**Solution:**
```bash
# Make scripts executable
chmod +x setup-ralph.sh ralph-execute.sh

# Verify permissions
ls -la *.sh
```

### Issue: Setup script fails during git commit

**Solution:**
```bash
# Configure git user
git config --global user.email "your@email.com"
git config --global user.name "Your Name"

# Try setup again
./setup-ralph.sh test-project
```

### Issue: Template files not copied

**Solution:**
```bash
# Verify templates directory exists
ls -la templates/

# If missing, check you're in the ralph-gemini directory
pwd  # Should end with /ralph-gemini
```

## Success Criteria

ralph-gemini is verified and ready to use if:

1. ✅ All scripts run without errors
2. ✅ Projects are created with complete file structure
3. ✅ Documentation is clear and comprehensive
4. ✅ Examples work as described
5. ✅ Scripts handle edge cases gracefully
6. ✅ Gemini CLI integration is properly documented

## Next Steps After Verification

Once verification is complete:

1. Read the [QUICKSTART.md](QUICKSTART.md) guide
2. Try the [simple-calculator example](examples/simple-calculator/)
3. Create your first Ralph project
4. Share feedback and improvements

## Reporting Issues

If you find any issues during verification:

1. Check the [Troubleshooting section in README](README.md#-troubleshooting)
2. Search existing GitHub issues
3. Create a new issue with:
   - Steps to reproduce
   - Expected vs actual behavior
   - Environment details (OS, Node version, Gemini CLI version)
   - Relevant logs or error messages

---

**Last Updated**: January 2026  
**Version**: 1.0.0
