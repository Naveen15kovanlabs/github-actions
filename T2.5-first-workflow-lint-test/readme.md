# T2.5 – First GitHub Actions Workflow: Lint + Test

## 1. Overview

This task demonstrates a Continuous Integration (CI) workflow using GitHub Actions.

The workflow automatically performs code quality checks and executes automated tests whenever code is pushed to the `main` branch or a Pull Request is created.

A dummy AI Incident Analyzer Python project is used to demonstrate the CI pipeline.

## 2. Objectives

- Create a GitHub Actions workflow using YAML.
- Configure workflow triggers for `push` and `pull_request`.
- Automate Python code linting using Ruff.
- Execute automated test cases using Pytest.
- Run Lint and Test as independent CI jobs.
- Verify successful workflow execution through GitHub Actions.
- Understand Pull Request checks and branch protection using Rulesets.

## 3. Technologies Used

| Technology | Purpose |
|---|---|
| GitHub Actions | CI workflow automation |
| Python 3.12 | Application runtime |
| Ruff | Code linting |
| Pytest | Automated testing |
| YAML | Workflow configuration |
| Git & GitHub | Version control |

## 4. Workflow Triggers

The workflow runs automatically on:

- **Push:** When code is pushed to the `main` branch.
- **Pull Request:** When a Pull Request is opened or updated.

## 5. CI Pipeline Architecture

```text
Developer pushes code
         |
         v
   GitHub Repository
         |
         v
    GitHub Actions
         |
    +----+----+
    |         |
    v         v
   Lint      Test
    |         |
   Ruff     Pytest
    |         |
    v         v
 Code Check  Test Results
    |         |
    +----+----+
         |
         v
   CI Results
```

## 6. Workflow Jobs

### Job 1: Lint

- Checks Python code using Ruff.
- Identifies code quality and formatting issues.
- Reports linting failures in GitHub Actions.

Command:

```bash
ruff check .
```

### Job 2: Test

- Executes automated test cases using Pytest.
- Validates application functionality.
- Reports passed and failed test cases.

Command:

```bash
python -m pytest -v
```

Both jobs run independently on GitHub-hosted Ubuntu runners.

## 7. Project Structure

```text
github-actions-practice/
├── app/
├── tests/
│   └── test_analyzer.py
├── pyproject.toml
├── requirements.txt
└── README.md
```

## 8. Local Validation

Before pushing the code, both checks were executed locally.

```bash
ruff check .
python -m pytest -v
```

**Test Result:** 5 test cases passed successfully.

**Lint Result:** All checks passed.

## 9. GitHub Actions Execution Results

The workflow was successfully triggered through both Push and Pull Request events.

- Lint job – Successful
- Test job – Successful
- Pull Request CI checks – Successful

## 10. Key Learnings

- Understanding GitHub Actions workflow structure.
- Configuring push and Pull Request triggers.
- Understanding jobs, steps, runners, and actions.
- Automating linting and testing.
- Understanding CI status checks.
- Learning how branch Rulesets can enforce required checks before merging.

## 11. Workflow Configuration

The actual workflow configuration is maintained in:

`workflow/ci.yml`

This is a reference copy of the workflow used in the separate practice repository.

---

**Status:** Completed

**Category:** CI/CD | GitHub Actions | DevOps