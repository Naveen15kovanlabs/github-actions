# What I Learned – GitHub Actions (Lint + Test)

While working on this task, I learned how to create a basic CI pipeline using GitHub Actions.

### 1. GitHub Actions
- Learned how GitHub Actions helps automate tasks.
- Understood how workflows run automatically when code is pushed or a Pull Request is created.

### 2. Workflow File
- Learned that GitHub Actions workflows are written in YAML.
- Understood why workflow files are stored inside `.github/workflows/`.

### 3. Workflow Triggers
- Learned how to trigger workflows using `push` and `pull_request`.
- Understood how GitHub automatically starts the workflow when these events happen.

### 4. Jobs and Steps
- Understood what jobs and steps mean.
- Learned that one workflow can contain multiple jobs.
- Created two separate jobs: Lint and Test.

### 5. Runner
- Learned what a runner is.
- Understood how GitHub provides an Ubuntu machine to execute workflow jobs.

### 6. Python Setup
- Learned how to set up Python 3.12 in GitHub Actions.
- Understood how to install project dependencies using `requirements.txt`.

### 7. Linting with Ruff
- Learned how Ruff checks Python code for common issues.
- Used `ruff check .` to check the project code.

### 8. Testing with Pytest
- Learned how Pytest runs automated test cases.
- Used `python -m pytest -v` to verify the application.
- Successfully executed all 5 test cases.

### 9. Pull Request Checks
- Learned how GitHub Actions runs checks when a Pull Request is created.
- Understood how to view successful and failed checks in GitHub.

### 10. GitHub Rulesets
- Learned how Rulesets help protect the main branch.
- Understood how required status checks can prevent merging when CI checks fail.

### Final Outcome

Successfully created and tested a GitHub Actions workflow that automatically runs Ruff linting and Pytest on push and Pull Request events.

**My main takeaway:** I now understand how code can be checked automatically before it gets merged into the main branch.