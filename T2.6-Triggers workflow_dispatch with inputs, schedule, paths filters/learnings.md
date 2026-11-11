# T2.6 – Learnings

## What I Learned

### 1. workflow_dispatch
- Learned how to trigger GitHub Actions workflows manually.
- Understood how to define custom inputs such as environment selection and boolean values.
- Learned how input values can control workflow execution.

### 2. Scheduled Workflows
- Learned how to use cron expressions to schedule automated workflows.
- Understood that GitHub Actions uses UTC for scheduled execution.
- Learned that scheduled runs may be delayed and are not guaranteed to start at the exact scheduled minute.

### 3. Path Filters
- Learned how to use `paths` filters with `push` and `pull_request` events.
- Understood how to trigger workflows only when specified files or folders are modified.
- Learned how patterns such as `**/*.py` match Python files across directories.

### 4. Workflow Jobs and Conditions
- Understood how to organize workflows into separate jobs for linting and testing.
- Learned how to use conditional expressions to skip the test job when manual input disables testing.
- Practiced using GitHub Actions event information to identify the trigger type.

## Key Takeaways

- Manual triggers provide control over workflow execution.
- Scheduled triggers help automate repetitive tasks.
- Path filters avoid unnecessary workflow executions.
- Cron expressions make it possible to schedule workflows at regular intervals.
- Separating linting and testing makes CI workflows easier to manage and maintain.

## Practical Experience

Implemented these triggers in a Python project and practiced checking workflow execution details, event types, inputs, and job results in the GitHub Actions interface.