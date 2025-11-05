# GitHub Actions Debugging and Logging Demo Lab

## Overview

This lab demonstrates various GitHub Actions debugging and logging capabilities using workflow commands. It's designed to showcase best practices for troubleshooting, logging, and managing workflow output.

## Prerequisites

Before running this demo, ensure you have:

1. **Environment Variables Set**: The following environment variables should be configured in your repository settings under `Settings > Environments > test`:
   - `ACTIONS_RUNNER_DEBUG` = `true`
   - `ACTIONS_STEP_DEBUG` = `true`

2. **Repository Access**: Ensure you have the necessary permissions to run workflows in the repository.

## What This Demo Covers

### 1. Basic Logging (`basic-logging-demo` job)
- **Echo Commands**: Standard output using `echo`
- **Debug Messages**: Using `::debug::` command (only visible when `ACTIONS_STEP_DEBUG=true`)
- **Warning Messages**: Using `::warning::` command with file/line annotations
- **Error Messages**: Using `::error::` command (non-failing for demo purposes)

### 2. Workflow Commands (`workflow-commands-demo` job)
- **Environment Variables**: Setting variables using `$GITHUB_ENV`
- **PATH Modification**: Adding directories using `$GITHUB_PATH`
- **Secret Masking**: Using `::add-mask::` to hide sensitive data
- **Job Summaries**: Creating markdown summaries using `$GITHUB_STEP_SUMMARY`

### 3. Log Organization (`log-grouping-demo` job)
- **Log Grouping**: Using `::group::` and `::endgroup::` for organized output
- **Nested Groups**: Demonstrating hierarchical log organization
- **System Information**: Practical examples of grouped system data

### 4. Advanced Commands (`advanced-commands-demo` job)
- **Command Control**: Using `::stop-commands::` and `::resume-commands::`
- **Output Parameters**: Setting and using step outputs
- **State Management**: Using `$GITHUB_STATE` for cleanup coordination

### 5. Conditional Logic (`conditional-logging-demo` job)
- **Input-Based Behavior**: Different logging based on workflow inputs
- **Error Simulation**: Optional failure demonstration
- **Success Path**: Conditional success messaging

### 6. GitHub CLI Integration (`github-cli-integration` job)
- **Repository Information**: Using `gh` CLI to fetch repo data
- **Workflow History**: Displaying recent workflow runs
- **Final Summary**: Comprehensive demo completion report

## How to Run the Demo

### Method 1: Manual Trigger (Recommended for Demo)

1. Navigate to your repository on GitHub
2. Go to **Actions** tab
3. Select **Debugging and Logging Demo** workflow
4. Click **Run workflow**
5. Configure inputs:
   - **Log Level**: Choose from `debug`, `info`, `warning`, or `error`
   - **Simulate Failure**: Check to demonstrate error handling

### Method 2: API Trigger

```bash
# Using GitHub CLI
gh workflow run debugging-and-logging-demo.yml \
  --field log_level=debug \
  --field simulate_failure=false

# Using curl
curl -X POST \
  -H "Authorization: token YOUR_TOKEN" \
  -H "Accept: application/vnd.github.v3+json" \
  https://api.github.com/repos/OWNER/REPO/actions/workflows/debugging-and-logging-demo.yml/dispatches \
  -d '{"ref":"main","inputs":{"log_level":"debug","simulate_failure":"false"}}'
```

## Key Learning Points

### Workflow Commands Format
```bash
echo "::command param1=value,param2=value::message"
```

### Essential Commands
- `::debug::` - Debug information (requires `ACTIONS_STEP_DEBUG=true`)
- `::notice::` - General notices
- `::warning::` - Warning messages
- `::error::` - Error messages
- `::group::` / `::endgroup::` - Log grouping
- `::add-mask::` - Hide sensitive data
- `::stop-commands::` / `::resume-commands::` - Control command processing

### Environment Files
- `$GITHUB_ENV` - Set environment variables
- `$GITHUB_PATH` - Modify PATH
- `$GITHUB_OUTPUT` - Set step outputs
- `$GITHUB_STEP_SUMMARY` - Add to job summary
- `$GITHUB_STATE` - Save state information

## Demo Script for Presenters

### Introduction (2 minutes)
1. Explain the purpose of debugging in CI/CD
2. Show the environment variables setup
3. Introduce the workflow structure

### Basic Logging (3 minutes)
1. Run the workflow with `log_level=debug`
2. Show the different message types in the output
3. Explain when each type should be used

### Advanced Features (5 minutes)
1. Demonstrate log grouping for organization
2. Show secret masking functionality
3. Explain environment variable setting
4. Show the job summary feature

### Interactive Elements (5 minutes)
1. Re-run with `simulate_failure=true`
2. Show error handling and conditional logic
3. Demonstrate different log levels
4. Review the final summary

### Q&A and Exploration (5 minutes)
1. Encourage attendees to examine the workflow file
2. Discuss real-world applications
3. Answer questions about implementation

## Real-World Applications

### Use Cases for These Techniques
1. **Debugging Failed Builds**: Use debug messages to trace execution
2. **Security**: Mask secrets and sensitive information
3. **Organization**: Group related operations for clarity
4. **Reporting**: Generate summaries for stakeholders
5. **Conditional Logic**: Handle different environments or scenarios
6. **Tool Integration**: Combine with GitHub CLI for advanced operations

### Best Practices
1. **Don't Overuse Debug**: Only when necessary for troubleshooting
2. **Group Related Operations**: Makes logs more readable
3. **Always Mask Secrets**: Prevent accidental exposure
4. **Use Meaningful Messages**: Help future debugging efforts
5. **Leverage Job Summaries**: Provide high-level status information

## Extension Ideas

1. **Add Performance Monitoring**: Time operations and log durations
2. **Integration with External Tools**: Send logs to monitoring systems
3. **Custom Actions**: Create reusable debugging actions
4. **Matrix Builds**: Show debugging across different environments
5. **Artifact Management**: Log and store debug information

## Troubleshooting

### Common Issues
1. **Debug Messages Not Visible**: Ensure `ACTIONS_STEP_DEBUG=true`
2. **Environment Variables Not Set**: Check repository settings
3. **Permissions Issues**: Verify workflow permissions
4. **CLI Authentication**: Ensure `GITHUB_TOKEN` has proper scope

### Additional Resources
- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Workflow Commands Reference](https://docs.github.com/en/actions/using-workflows/workflow-commands-for-github-actions)
- [Debugging Workflows](https://docs.github.com/en/actions/monitoring-and-troubleshooting-workflows/enabling-debug-logging)