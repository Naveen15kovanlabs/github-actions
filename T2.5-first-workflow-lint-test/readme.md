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
- Identifies code quality issues.
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

**Lint command:**

```bash
ruff check .
```

**Test command:**

```bash
python -m pytest -v
```

**Results:**
- Test Result: All 5 test cases passed successfully.
- Lint Result: All checks passed.

## 9. GitHub Actions Execution Results

The workflow was successfully triggered through both Push and Pull Request events.

- Lint job – Successful
- Test job – Successful
- Pull Request CI checks – Successful

### 9.1 GitHub Actions Workflow

![GitHub Actions workflow](screenshots/Screenshot%20(748).png)

### 9.2 Lint Job Execution

![Lint job execution](screenshots/Screenshot%20(749).png)

### 9.3 Test Job Execution

![Test job execution](screenshots/Screenshot%20(750).png)

### 9.4 Pull Request CI Checks

![Pull Request CI checks](screenshots/Screenshot%20(751).png)

## 10. GitHub Rulesets and Branch Protection

GitHub Rulesets help protect the `main` branch by defining rules that must be followed before changes can be merged.

Configured protections include:

- Require a Pull Request before merging.
- Require status checks to pass.
- Configure Lint and Test as required status checks.

### 10.1 Ruleset Configuration

![GitHub Ruleset configuration](screenshots/Screenshot%20(752).png)

### 10.2 Required Status Checks

![Required status checks](screenshots/Screenshot%20(753).png)

## 11. Key Learnings

- Understanding GitHub Actions workflow structure.
- Configuring `push` and `pull_request` triggers.
- Understanding jobs, steps, runners, and actions.
- Automating code linting and testing.
- Understanding CI status checks.
- Learning how GitHub Rulesets help protect branches.

## 12. Workflow Configuration

The workflow configuration is maintained in:

`workflow/ci.yml`

This is a reference copy of the actual workflow used in the separate practice repository.

## 13. Final Outcome

Successfully created and tested a GitHub Actions CI workflow that automatically runs Ruff linting and Pytest whenever code is pushed or a Pull Request is created.

**Status:** Completed

**Category:** CI/CD | GitHub Actions | DevOps