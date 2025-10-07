# GitHub Actions Job Context Testing

A comprehensive repository demonstrating practical examples of GitHub Actions job context usage. This repository contains multiple workflow files that showcase different aspects of the `job` context and related GitHub Actions features.

## Overview

The GitHub Actions `job` context contains information about the currently running job. This repository provides real-world examples of how to use job context effectively in your workflows.

## Workflows

### 1. Job Context Basics (`job-context-basics.yml`)

Demonstrates fundamental job context properties:
- Accessing `job.status`
- Accessing `job.check_run_id`
- Displaying the complete job context as JSON
- Showing related context information (runner, github)

**Triggers**: Push to main, Pull Requests, Manual dispatch

```yaml
echo "Job Status: ${{ job.status }}"
echo '${{ toJSON(job) }}'
```

### 2. Job Context Status Handling (`job-context-status.yml`)

Shows how to handle different job statuses:
- Successful jobs
- Jobs with failures (using `continue-on-error`)
- Cleanup jobs that run regardless of previous job outcomes
- Using `needs` context to check results of dependent jobs

**Key Features**:
- `if: always()` - runs regardless of previous step/job status
- `needs.<job>.result` - check the result of dependent jobs
- `continue-on-error` - allow jobs to continue after failures

### 3. Job Context Matrix Strategy (`job-context-matrix.yml`)

Demonstrates job context with matrix builds:
- Multiple OS platforms (Ubuntu, Windows, macOS)
- Multiple Node.js versions
- Matrix includes for special configurations
- Summarizing matrix job results

**Matrix Configuration**:
```yaml
strategy:
  matrix:
    os: [ubuntu-latest, windows-latest, macos-latest]
    node-version: [16, 18, 20]
```

### 4. Job Context Container Services (`job-context-containers.yml`)

Shows job context when using containers and services:
- Running jobs in Docker containers
- Using service containers (Redis, PostgreSQL)
- Accessing container and service context information
- Testing service connectivity

**Example Services**:
- Redis for caching
- PostgreSQL for databases

### 5. Job Context Dependencies (`job-context-dependencies.yml`)

Demonstrates job dependencies and data flow:
- Job outputs and how to pass data between jobs
- Sequential job execution with `needs`
- Conditional deployment based on previous job results
- Comprehensive notification job that summarizes all results

**Job Pipeline**:
```
build → test → deploy-staging → deploy-production
                                        ↓
                                     notify
```

### 6. Job Context Conditional Execution (`job-context-conditionals.yml`)

Shows various conditional execution patterns:
- Step-level conditionals (`if: success()`, `if: failure()`, `if: always()`)
- Job-level conditionals based on events
- Branch-specific jobs
- Actor-specific logic (e.g., Dependabot detection)
- Workflow dispatch with input parameters

**Conditional Types**:
- `if: success()` - runs only if previous steps succeeded
- `if: failure()` - runs only if a previous step failed
- `if: always()` - runs regardless of previous outcomes
- `if: cancelled()` - runs only if workflow was cancelled

## Key Job Context Properties

| Property | Description |
|----------|-------------|
| `job.status` | The current status of the job |
| `job.check_run_id` | The ID of the check run associated with this job |
| `job.container.id` | The ID of the job's container |
| `job.container.network` | The network ID of the job's container |
| `job.services` | Service containers created for the job |

## Related Contexts

These workflows also demonstrate usage of related contexts:

- **`github` context**: Repository, workflow, and event information
- **`runner` context**: Information about the runner (OS, architecture)
- **`needs` context**: Outputs and results from dependent jobs
- **`matrix` context**: Current matrix configuration values

## Usage

### Trigger Workflows Manually

All workflows can be triggered manually via the Actions tab:
1. Go to the "Actions" tab in this repository
2. Select the workflow you want to run
3. Click "Run workflow"
4. (For conditionals workflow) Select environment if prompted

### Trigger Workflows via Git

Push to main branch or create a pull request to trigger workflows:

```bash
git add .
git commit -m "Test workflows"
git push origin main
```

## Learning Resources

- [GitHub Actions Contexts](https://docs.github.com/en/actions/learn-github-actions/contexts)
- [Job Context Reference](https://docs.github.com/en/actions/learn-github-actions/contexts#job-context)
- [Workflow Syntax](https://docs.github.com/en/actions/using-workflows/workflow-syntax-for-github-actions)

## Examples from This Repository

### Example 1: Checking Job Status

```yaml
- name: Check job status
  run: echo "Current job status is ${{ job.status }}"
```

### Example 2: Conditional Step Execution

```yaml
- name: Cleanup on failure
  if: failure()
  run: echo "Performing cleanup after failure"
```

### Example 3: Accessing Dependent Job Results

```yaml
- name: Display previous job results
  run: |
    echo "Build result: ${{ needs.build.result }}"
    echo "Test result: ${{ needs.test.result }}"
```

### Example 4: Matrix Configuration Access

```yaml
- name: Display matrix values
  run: |
    echo "OS: ${{ matrix.os }}"
    echo "Version: ${{ matrix.node-version }}"
```

## Contributing

Feel free to add more examples or improve existing workflows! Create a pull request with your changes.

## License

This repository is for educational purposes.