# GitHub Actions Workflow Commands Quick Reference

## 🔧 Command Syntax
```
echo "::command param1=value,param2=value::message"
```

## 📝 Basic Logging Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `::debug::` | Debug information | `echo "::debug::Variable value: $VAR"` |
| `::notice::` | General notices | `echo "::notice::Build completed successfully"` |
| `::warning::` | Warning messages | `echo "::warning::Deprecated feature used"` |
| `::error::` | Error messages | `echo "::error::Configuration file missing"` |

## 📁 Log Organization

| Command | Purpose | Example |
|---------|---------|---------|
| `::group::` | Start log group | `echo "::group::Installing Dependencies"` |
| `::endgroup::` | End log group | `echo "::endgroup::"` |

## 🔒 Security Commands

| Command | Purpose | Example |
|---------|---------|---------|
| `::add-mask::` | Hide sensitive data | `echo "::add-mask::$SECRET"` |
| `::stop-commands::` | Pause command processing | `echo "::stop-commands::token123"` |
| `::resume-commands::` | Resume command processing | `echo "::resume-commands::token123"` |

## 🔧 Environment Management

| File | Purpose | Example |
|------|---------|---------|
| `$GITHUB_ENV` | Set environment variables | `echo "VAR=value" >> $GITHUB_ENV` |
| `$GITHUB_PATH` | Modify PATH | `echo "/custom/bin" >> $GITHUB_PATH` |
| `$GITHUB_OUTPUT` | Set step outputs | `echo "result=success" >> $GITHUB_OUTPUT` |
| `$GITHUB_STEP_SUMMARY` | Add to job summary | `echo "# Summary" >> $GITHUB_STEP_SUMMARY` |
| `$GITHUB_STATE` | Save state | `echo "cleanup=true" >> $GITHUB_STATE` |

## 📍 File Annotations

### Warning with Location
```bash
echo "::warning file=config.yml,line=15,col=3::Missing required field"
```

### Error with Location
```bash
echo "::error file=src/main.js,line=42::Undefined variable 'foo'"
```

### Notice with Title
```bash
echo "::notice title=Build Status::All tests passed successfully"
```

## 🐛 Debug Environment Variables

Set these in your repository environment settings:

| Variable | Purpose |
|----------|---------|
| `ACTIONS_RUNNER_DEBUG=true` | Enable runner debugging |
| `ACTIONS_STEP_DEBUG=true` | Enable step debugging |

## 💡 Best Practices

### ✅ Do
- Always mask secrets with `::add-mask::`
- Group related operations for better readability
- Use meaningful error messages with file locations
- Leverage job summaries for high-level status
- Use debug messages for troubleshooting

### ❌ Don't
- Expose sensitive information in logs
- Overuse debug messages in production workflows
- Create overly nested groups
- Use workflow commands for normal output
- Forget to resume commands after stopping

## 🎯 Common Patterns

### Error Handling
```bash
if ! command_that_might_fail; then
    echo "::error::Command failed with exit code $?"
    exit 1
fi
```

### Conditional Debug
```bash
if [[ "$DEBUG" == "true" ]]; then
    echo "::debug::Detailed debugging information"
fi
```

### Grouped Operations
```bash
echo "::group::Setup Phase"
echo "Installing dependencies..."
npm install
echo "Configuring environment..."
cp config.example.json config.json
echo "::endgroup::"
```

### Setting Outputs
```bash
# Modern way (recommended)
echo "build-version=$(cat version.txt)" >> $GITHUB_OUTPUT

# Using in another step
echo "Version: ${{ steps.step-id.outputs.build-version }}"
```

### Job Summary
```bash
echo "## Build Results 📊" >> $GITHUB_STEP_SUMMARY
echo "- Status: ✅ Success" >> $GITHUB_STEP_SUMMARY
echo "- Duration: 2m 30s" >> $GITHUB_STEP_SUMMARY
echo "- Tests: 42 passed, 0 failed" >> $GITHUB_STEP_SUMMARY
```

## 🔗 References

- [Official Workflow Commands Documentation](https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions)
- [Debugging GitHub Actions](https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/enabling-debug-logging)
- [Environment Variables](https://docs.github.com/en/actions/learn-github-actions/variables)