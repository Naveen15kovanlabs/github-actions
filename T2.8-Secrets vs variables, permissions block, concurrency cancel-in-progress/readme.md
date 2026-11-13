# T2.8 – Secrets vs Variables, Permissions and Concurrency

## Overview

In this task, I worked on improving the security and execution management of GitHub Actions workflows.

I learned how to handle secrets and variables, configure workflow permissions, and manage multiple workflow runs using concurrency controls.

I created a separate workflow file for this task without modifying my previous CI workflow.

## Screenshots and Implementation Evidence

### 1. Repository Secret Configuration

I configured a repository secret named `GROQ_API_KEY` under Settings → Secrets and variables → Actions. This helps me store sensitive API credentials securely instead of directly adding them to the workflow YAML file.

![Repository Secret Configuration](https://github.com/Naveen15github/github-actions/blob/14baf858d24e6047ac14d87df58aba7266520db9/T2.8-Secrets%20vs%20variables%2C%20permissions%20block%2C%20concurrency%20cancel-in-progress/images/Screenshot%202026-11-13%20142516.png)

### 2. Permissions and Concurrency Configuration

I added a permissions block with `contents: read` to keep the default workflow token access read-only.

I also configured concurrency using a group based on the workflow and pull request number or branch reference. With `cancel-in-progress: true`, older running workflows in the same group are cancelled when a new run starts.

![Permissions and Concurrency Configuration](https://github.com/Naveen15github/github-actions/blob/14baf858d24e6047ac14d87df58aba7266520db9/T2.8-Secrets%20vs%20variables%2C%20permissions%20block%2C%20concurrency%20cancel-in-progress/images/Screenshot%20%28770%29.png)

### 3. Successful Workflow Execution

After configuring the workflow, I triggered a run and verified that the workflow completed successfully.

The verification job finished without failure, confirming that the workflow configuration was working.

![Successful GitHub Actions Workflow](https://github.com/Naveen15github/github-actions/blob/14baf858d24e6047ac14d87df58aba7266520db9/T2.8-Secrets%20vs%20variables%2C%20permissions%20block%2C%20concurrency%20cancel-in-progress/images/Screenshot%20%282026-11-13%20143119%29.png)

## What I Implemented

### 1. Secrets vs Variables

- Used GitHub repository secrets to store sensitive information.
- Configured `GROQ_API_KEY` as a repository secret.
- Used GitHub Actions variables for normal configuration values.
- Accessed these values through the GitHub Actions expressions.
- Avoided hardcoding sensitive credentials in the workflow file.

### 2. Permissions Block

Configured the following permission:

```yaml
permissions:
  contents: read
```

This gives the workflow read-only access to repository contents by default.

It follows the principle of least privilege, where a workflow receives only the permissions it needs.

### 3. Concurrency Control

Configured the following:

```yaml
concurrency:
  group: ${{ github.workflow }}-${{ github.event.pull_request.number || github.ref }}
  cancel-in-progress: true
```

- `group`: Groups workflow runs based on the workflow and pull request or branch.
- `cancel-in-progress: true`: Cancels older running jobs when a newer run starts in the same group.

This helps avoid unnecessary workflow executions and reduces resource usage.

## What I Learned

- I understood the difference between GitHub Actions secrets and variables.
- I learned how to store API keys securely in repository settings.
- I understood how the `permissions` block controls the access given to `GITHUB_TOKEN`.
- I learned why read-only permissions are safer as a default.
- I understood how concurrency groups work in GitHub Actions.
- I learned how `cancel-in-progress` helps manage multiple workflow runs.
- I understood how these configurations improve CI/CD workflow security and execution management.

## Advantages

- Sensitive credentials are stored securely.
- Reduces the risk of exposing API keys in workflow files.
- Read-only permissions help prevent unwanted repository changes.
- Concurrency control avoids unnecessary workflow runs.
- Makes CI/CD pipelines more secure and manageable.

## Challenges / Things to Understand

- Secrets cannot be viewed again as plain text after saving them in GitHub.
- Incorrect permissions can cause workflow steps to fail.
- Concurrency groups must be configured properly to avoid cancelling unrelated workflow runs.

## Final Result

Successfully implemented and tested a separate GitHub Actions workflow for T2.8 covering secrets and variables handling, read-only workflow permissions, and concurrency cancellation.

The workflow execution completed successfully, and I verified the main configuration through GitHub repository settings and Actions run details.