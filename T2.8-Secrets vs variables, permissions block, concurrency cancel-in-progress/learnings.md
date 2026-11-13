# T2.8 – Learnings: Secrets vs Variables, Permissions and Concurrency

## What I Learned

In this task, I learned how to make GitHub Actions workflows more secure and how to manage multiple workflow runs properly.

### 1. Secrets vs Variables

- I learned that secrets are used to store sensitive information like API keys, passwords and tokens.
- Variables are used for normal configuration values like application names and environment names.
- I configured a repository secret named `GROQ_API_KEY`.
- I understood that storing API keys in GitHub Secrets is safer than directly writing them inside YAML files.

### 2. Permissions Block

- I learned how permissions control what a GitHub Actions workflow can access or modify.
- I used `contents: read` to give the workflow read-only access to repository contents.
- I understood that we should not give unnecessary permissions to workflows.
- This helps improve workflow security and reduces unwanted access.

### 3. Concurrency Control

- I learned how multiple workflow runs can happen when we push changes repeatedly.
- I understood how concurrency groups help manage these workflow runs.
- I used `cancel-in-progress: true` to cancel older running workflows when a new run starts in the same group.
- This helps avoid running unnecessary workflows and saves resources.

## Advantages (Pros)

- Secrets help protect sensitive information like API keys and passwords.
- Variables make it easier to manage normal configuration values.
- Read-only permissions provide better security.
- Concurrency control avoids unnecessary workflow executions.
- Cancelling older runs saves time and GitHub Actions resources.
- These features make CI/CD workflows easier to manage.

## Disadvantages (Cons)

- If a secret name is incorrect, the workflow may not get the expected value.
- Secrets cannot be viewed again as plain text after saving them.
- Incorrect permissions can cause workflow steps to fail.
- If concurrency groups are not configured properly, important running jobs may get cancelled.
- Debugging workflows can sometimes be difficult because secret values are hidden in logs.

## My Practical Understanding

Before this task, I knew how to create and run GitHub Actions workflows, but I did not have much practical experience with workflow security and concurrency.

After implementing this task, I understood why we should keep sensitive values separate from YAML files, why workflows should have minimum permissions, and how to handle multiple workflow runs.

I also understood that a successful workflow execution alone is not enough. We should configure the workflow securely and make sure it behaves properly when multiple runs happen.

## Final Learning

This task helped me understand some important security and execution management practices used in real-world CI/CD pipelines. I can now apply secrets, variables, permissions and concurrency controls when creating GitHub Actions workflows for future projects.