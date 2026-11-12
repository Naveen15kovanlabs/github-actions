# T2.7 – Matrix, Cache, Artifacts, Needs + Job Outputs, If Conditions

## Overview

In this task, I implemented an advanced GitHub Actions workflow to understand how to manage multiple jobs, optimize workflow execution, share data between jobs, and preserve generated files.

I created a separate workflow named `matrix-cache-artifacts.yml` without modifying my existing CI workflow.

The implementation covers:

- Matrix Strategy – Run tests using multiple Python versions.
- Dependency Caching – Cache Python dependencies to reduce installation time.
- Artifacts – Generate and upload test reports.
- Needs – Define dependencies between workflow jobs.
- Job Outputs – Pass values from one job to another.
- If Conditions – Control job and step execution based on conditions.

**Main objective:** Implement these features and verify whether a subsequent workflow execution becomes faster through dependency caching.

## 1. Workflow Architecture

I designed the workflow with separate jobs to keep the execution organized and demonstrate job dependencies.

The workflow consists of:

1. Prepare Test Matrix – Define Python versions and expose them as job outputs.
2. Lint Python Code – Run Ruff to check code quality.
3. Matrix Testing – Execute tests using Python 3.11 and Python 3.12.
4. Summarize Workflow Results – Collect job results and generate a workflow summary.

The matrix testing jobs can execute in parallel, while the summary job waits for its required jobs using `needs`.

![Successful GitHub Actions workflow execution](images/Screenshot%20(766).png)

*Figure 1: Successful workflow execution showing the job structure, matrix testing and summary job.*

## 2. Matrix Strategy

I implemented GitHub Actions Matrix Strategy to test the Python application using multiple Python versions without creating separate workflow definitions for each version.

Configured Python versions:

- Python 3.11
- Python 3.12

I used a matrix configuration to generate separate test jobs automatically.

**Implementation highlights:**
- Used a matrix to define multiple Python versions.
- Passed the Python version dynamically to the setup-python action.
- Executed the test suite independently for each version.
- Allowed the matrix jobs to run in parallel.

This helped me understand how matrix strategy reduces duplicate workflow configuration and supports testing across multiple environments.

## 3. Workflow Execution Time

After executing the workflow, I checked the GitHub Actions Usage section to understand the execution time of individual jobs.

The recorded job timings were:

| Job | Execution time |
|---|---:|
| Prepare test matrix | 3 seconds |
| Lint Python code | 22 seconds |
| Test with Python 3.12 | 37 seconds |
| Test with Python 3.11 | 36 seconds |
| Summarize workflow results | 4 seconds |

The workflow summary showed an overall duration of approximately 51 seconds.

The Usage page showed a combined job runtime of 1 minute 42 seconds. This is the sum of individual job runtimes, not the elapsed wall-clock duration of the workflow, because some jobs run in parallel.

![GitHub Actions workflow usage](images/Screenshot%20(767).png)

*Figure 2: Individual job execution times in GitHub Actions Usage.*

## 4. Dependency Caching

I implemented Python dependency caching using the `actions/setup-python@v5` action.

I configured pip caching with dependency files such as:

- `requirements.txt`
- `pyproject.toml`

The cache allows GitHub Actions to reuse previously downloaded Python packages in subsequent workflow executions.

**First execution:**
- Dependencies are downloaded and installed.
- GitHub Actions creates the dependency cache.

**Subsequent execution:**
- GitHub Actions checks for an existing cache.
- Matching cached dependencies are restored.
- Pip can reuse cached packages during installation.

I verified the cache restoration in the workflow logs.

![Python dependency cache restoration](images/Screenshot%202026-11-12%20132843.png)

*Figure 3: GitHub Actions successfully restoring the Python pip cache.*

I also checked the dependency installation output.

The log showed:

- Dependency installation elapsed: 15 seconds.
- Pip cache hit: `true`.

This confirmed that the workflow successfully restored the existing dependency cache.

![Pip cache hit and dependency installation output](images/Screenshot%202026-11-12%20132904.png)

*Figure 4: Dependency installation output confirming a successful cache hit.*

**Observation:** A cache hit does not mean that pip installation is skipped. It means previously downloaded packages can be reused, reducing unnecessary downloads.

## 5. Artifacts

I implemented artifact uploading to preserve the test reports generated during matrix testing.

For each Python version, the workflow generates a pytest XML report.

I used `actions/upload-artifact@v4` to upload the reports after test execution.

Generated artifacts:

- `test-reports-python-3.11`
- `test-reports-python-3.12`

These reports are available in the Artifacts section of the completed GitHub Actions run.

![Uploaded test report artifacts](images/Screenshot%202026-11-12%20133230.png)

*Figure 5: Successfully uploaded test report artifacts for both Python versions.*

This helped me understand how workflow-generated files can be stored and downloaded after a job completes.

## 6. Needs and Job Outputs

I implemented job dependencies using the `needs` keyword.

This ensures that dependent jobs execute only after their required jobs have completed.

I also used job outputs to share information between jobs.

**Implementation:**

- The prepare job defines the Python version matrix.
- The Python version information is exposed through job outputs.
- The matrix testing job consumes those outputs dynamically.
- The summary job uses job dependencies to collect the results of previous jobs.

This helped me understand how multiple jobs communicate and coordinate execution within a GitHub Actions workflow.

## 7. If Conditions

I used conditional execution to control workflow behavior.

The workflow includes a manual input named `run_tests` to control whether test execution should proceed.

I also used job and step conditions to handle execution based on the workflow inputs and previous job results.

This helps avoid unnecessary execution and provides better control over the workflow.

## 8. Final Verification and Observations

After implementing the workflow, I verified the following:

| Feature | Result |
|---|---|
| Matrix Strategy | Successfully tested Python 3.11 and 3.12 |
| Dependency Caching | Cache restoration confirmed |
| Artifacts | Two test report artifacts uploaded |
| Needs | Job dependencies configured |
| Job Outputs | Python versions passed between jobs |
| If Conditions | Conditional execution configured |
| Workflow Execution | Successful |

### Cache Performance Observation

I reviewed multiple workflow runs. The recorded overall durations were approximately:

- First inspected run: 50 seconds
- Second inspected run: 53 seconds
- Third inspected run: 53 seconds

Although the logs confirmed successful cache restoration and a 15-second dependency installation time, these overall durations do not demonstrate a measurable speed improvement.

All the inspected runs showed a cache hit, so I still need a controlled cold-cache versus warm-cache comparison.

**Next verification:**

1. Delete the relevant Python dependency cache entries from GitHub Actions cache settings.
2. Run the workflow and record the dependency installation time with `Pip cache hit: false`.
3. Run it again without changing the dependency files.
4. Confirm `Pip cache hit: true`.
5. Compare the dependency installation times for the same Python version.

I will use these measurements to determine the actual performance improvement rather than assuming that caching automatically makes every run faster.

## 9. Key Learnings

Through this task, I gained practical experience with:

- Implementing matrix builds for multiple Python versions.
- Optimizing dependency installation using pip caching.
- Uploading and managing workflow artifacts.
- Managing job execution order using `needs`.
- Passing dynamic values between jobs using job outputs.
- Controlling workflow execution using conditional expressions.
- Inspecting GitHub Actions logs and measuring workflow performance.

## Conclusion

I successfully implemented an advanced GitHub Actions workflow combining Matrix Strategy, dependency caching, artifacts, job dependencies, job outputs and conditional execution.

I verified successful workflow execution, matrix testing across two Python versions, cache restoration and artifact uploading.

I also learned how to inspect workflow execution timings and why controlled measurements are necessary to demonstrate actual CI pipeline optimization.