# T2.6 – GitHub Actions Workflow Triggers

## Overview

This task demonstrates different types of workflow triggers in GitHub Actions using a Python project.

The workflow is configured to run based on manual requests, scheduled intervals, and specific file changes.

## Triggers Implemented

### 1. workflow_dispatch – Manual Trigger
- Allows users to run the workflow manually from the GitHub Actions tab.
- Added an `environment` input with options: `dev`, `staging`, and `production`.
- Added a `run_tests` boolean input to control whether automated tests should run.

### 2. schedule – Scheduled Trigger
- Configured using a cron expression.
- Runs automatically every 5 minutes.

```yaml
schedule:
  - cron: "*/5 * * * *"
```

Note: GitHub scheduled workflows use UTC and may experience execution delays.

### 3. Path Filters
- Configured `push` and `pull_request` triggers for the `main` branch.
- Workflows run only when relevant files are changed.

Configured paths:
- `**/*.py`
- `requirements.txt`
- `pyproject.toml`
- `.github/workflows/**`

## Workflow Jobs

**Lint Job**
- Sets up Python 3.12.
- Installs project dependencies.
- Runs Ruff to check Python code quality.

**Test Job**
- Runs automated tests using pytest.
- Can be skipped during manual execution by setting `run_tests` to `false`.

## Testing and Verification

- Tested manual execution with custom inputs.
- Configured and verified scheduled execution.
- Tested Python file changes to demonstrate path-based triggering.
- Verified CI workflow execution through the GitHub Actions tab.

## Files

- `.github/workflows/workflow-triggers.yml` – Workflow configuration.

## Outcome

Successfully implemented and demonstrated manual, scheduled, and path-based workflow triggers using GitHub Actions.