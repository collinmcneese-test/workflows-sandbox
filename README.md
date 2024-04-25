# repo_with_a_workflow

Simple repository with a workflow file and an example [CODEOWNERS](.github/CODEOWNERS) to protect changes to this file ([more details on code owners](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners)).

Usage of `CODEOWNERS` additionally requires that Branch Protection rules be enabled.  As an example:

![image](https://user-images.githubusercontent.com/8185808/181379196-6ea86e04-1b18-45a5-a5e2-df3f65838d64.png)

## GitHub Actions Workflows

This section provides an overview of the GitHub Actions workflows defined in this repository under `.github/workflows`. These workflows automate various aspects of the development process, from code linting and testing to deployment.

### Table of Contents

- [all-echoes.yml](#all-echoes)
- [context.yml](#context)
- [dependabot-auto.yml](#dependabot-auto)
- [deploy.yml](#deploy)
- [dynamic-called.yml](#dynamic-called)
- [dynamic-matrix.yml](#dynamic-matrix)
- [echo1.yml](#echo1)
- [echo2.yml](#echo2)
- [echo3.yml](#echo3)
- [fail.yml](#fail)
- [failure.yml](#failure)
- [issue-labels.yml](#issue-labels)
- [issue-workflow-called.yml](#issue-workflow-called)
- [issues.yml](#issues)
- [my-workflow.yml](#my-workflow)
- [pr-against-default.yml](#pr-against-default)
- [pr-dependency-review.yml](#pr-dependency-review)
- [rate-limit.yml](#rate-limit)
- [release.yml](#release)
- [retry.yml](#retry)
- [scorecard.yml](#scorecard)
- [self-hosted-container.yml](#self-hosted-container)
- [self-hosted.yml](#self-hosted)
- [workflow-metrics.yml](#workflow-metrics)
- [workflow-with-protection-check.yml](#workflow-with-protection-check)

### all-echoes.yml

**Description:** This workflow demonstrates the use of reusable workflows by calling multiple echo workflows.

**Trigger Events:** Manual trigger via `workflow_dispatch`.

**Jobs:**
- **echo1, echo2, echo3:** Calls reusable echo workflows.
- **reporter:** Aggregates results from echo jobs and reports rate limits.

**Special Notes:** Utilizes reusable workflows for modular job execution.

### context.yml

**Description:** Prints GitHub context information for debugging purposes.

**Trigger Events:** Manual trigger via `workflow_dispatch` and on issue events (opened, edited).

**Jobs:**
- **context:** Prints the GitHub context to the console.

**Special Notes:** Useful for debugging and understanding GitHub context in actions.

### dependabot-auto.yml

**Description:** Automatically approves pull requests created by Dependabot.

**Trigger Events:** On pull request events.

**Jobs:**
- **dependabot:** Checks if the actor is Dependabot and approves the PR if conditions are met.

**Special Notes:** Ensures automated dependency updates are approved for further CI/CD processes.

### deploy.yml

**Description:** Manages deployment to various environments based on manual triggers.

**Trigger Events:** Manual trigger via `workflow_dispatch` with environment selection.

**Jobs:**
- **auto-deploy:** Automatically deploys to sandbox and dev environments on push to main.
- **deploy:** Deploys to a specified environment based on manual input.
- **deploy-all:** Deploys to all environments if 'all' is selected.

**Special Notes:** Demonstrates conditional job execution and environment deployments.

### dynamic-called.yml

**Description:** A reusable workflow that can be dynamically called with different inputs.

**Trigger Events:** Can be called by other workflows using `workflow_call`.

**Jobs:**
- **reusable-workflow:** Executes with dynamic inputs provided by the caller workflow.

**Special Notes:** Showcases the flexibility of reusable workflows with dynamic inputs.

### dynamic-matrix.yml

**Description:** Demonstrates the use of dynamic matrix strategies in GitHub Actions.

**Trigger Events:** Manual trigger via `workflow_dispatch` with options to run specific or all jobs.

**Jobs:**
- **outputs-static:** Generates a static output for use in other jobs.
- **run-with-json:** Uses the output from `outputs-static` to run jobs dynamically.
- **matrix-array:** Demonstrates dynamic job execution based on array outputs.
- **matrix-object:** Demonstrates dynamic job execution based on object outputs.

**Special Notes:** Highlights advanced CI/CD techniques with dynamic job configurations.

### echo1.yml

**Description:** A reusable workflow that echoes a message.

**Trigger Events:** Manual trigger via `workflow_dispatch` and can be called by other workflows.

**Jobs:**
- **call-echo1:** Calls the echo1 reusable workflow.

**Special Notes:** Part of a set of reusable echo workflows for demonstration purposes.

### echo2.yml

**Description:** Similar to echo1.yml, this reusable workflow echoes a message.

**Trigger Events:** Manual trigger via `workflow_dispatch` and can be called by other workflows.

**Jobs:**
- **call-echo2:** Calls the echo2 reusable workflow.

**Special Notes:** Part of a set of reusable echo workflows for demonstration purposes.

### echo3.yml

**Description:** Similar to echo1.yml and echo2.yml, this reusable workflow echoes a message.

**Trigger Events:** Manual trigger via `workflow_dispatch` and can be called by other workflows.

**Jobs:**
- **call-echo1:** Calls the echo1 reusable workflow (note: likely intended to call echo3).

**Special Notes:** Part of a set of reusable echo workflows for demonstration purposes. Note the potential typo in job name.

### fail.yml

**Description:** A simple workflow designed to fail for testing failure handling.

**Trigger Events:** Manual trigger via `workflow_dispatch`.

**Jobs:**
- **build:** Executes a script that exits with a failure status.

**Special Notes:** Useful for testing failure handling and retry mechanisms in workflows.

### failure.yml

**Description:** Simulates a workflow with multiple jobs, some of which are designed to fail.

**Trigger Events:** Manual trigger via `workflow_dispatch`.

**Jobs:**
- **job1, job2, job3, job4:** Various jobs with different configurations, some designed to fail.

**Special Notes:** Demonstrates handling of job failures and dependencies between jobs.

### issue-labels.yml

**Description:** Triggers actions based on issue labels.

**Trigger Events:** On issue events when labeled.

**Jobs:**
- **labeled:** Executes if the issue is labeled with 'duplicate'.

**Special Notes:** Showcases conditional job execution based on issue labels.

### issue-workflow-called.yml

**Description:** A workflow called by other workflows to handle issue-related actions.

**Trigger Events:** Can be called by other workflows using `workflow_call`.

**Jobs:**
- **issue-workflow-called:** Executes actions based on the calling workflow's context.

**Special Notes:** Enables modular handling of issue-related actions across workflows.

### issues.yml

**Description:** Tests issue-related events and outputs the GitHub context.

**Trigger Events:** On issue events (labeled, edited).

**Jobs:**
- **output:** Outputs the GitHub context for debugging.

**Special Notes:** Useful for understanding and debugging issue event handling.

### my-workflow.yml

**Description:** A customizable workflow that echoes a message with selected options.

**Trigger Events:** Manual trigger via `workflow_dispatch` with input options.

**Jobs:**
- **echo-selections:** Echoes the selected message and color to the console.

**Special Notes:** Demonstrates the use of workflow inputs for customization.

### pr-against-default.yml

**Description:** Handles pull requests against the default branch with specific actions.

**Trigger Events:** On pull request events.

**Jobs:**
- **env:** Outputs environment variables for debugging.
- **default-branch-pr:** Executes if the PR is against the default branch.
- **not-default-branch-pr:** Executes if the PR is not against the default branch.

**Special Notes:** Differentiates actions based on whether the PR targets the default branch.

### pr-dependency-review.yml

**Description:** Reviews dependencies in pull requests for security vulnerabilities.

**Trigger Events:** On pull request events.

**Jobs:**
- **dependency-review:** Reviews dependencies and fails on high severity vulnerabilities.

**Special Notes:** Enhances security by automatically reviewing dependencies in PRs.

### rate-limit.yml

**Description:** Checks GitHub API rate limits and outputs the results.

**Trigger Events:** Manual trigger via `workflow_dispatch`.

**Jobs:**
- **check-rate-limit:** Fetches and parses GitHub API rate limits, outputting them in a table.

**Special Notes:** Useful for monitoring and managing GitHub API usage.

### release.yml

**Description:** Handles actions upon creation of a new release.

**Trigger Events:** On release events (created).

**Jobs:**
- **release:** Executes actions specific to the release event.

**Special Notes:** Automates tasks related to new releases, such as notifications or deployments.

### retry.yml

**Description:** Retries a workflow upon failure, with a limit on retry attempts.

**Trigger Events:** On completion of specific workflows (e.g., failure-workflow).

**Jobs:**
- **retry:** Analyzes failed jobs and retries the workflow if conditions are met.
- **exhaust:** Executes if the workflow has exhausted its retry attempts.

**Special Notes:** Demonstrates advanced error handling and retry mechanisms in workflows.

### scorecard.yml

**Description:** Runs the Scorecard supply-chain security analysis on the repository.

**Trigger Events:** On branch protection rule events and scheduled runs.

**Jobs:**
- **analysis:** Performs the Scorecard analysis and uploads results.

**Special Notes:** Enhances supply-chain security by regularly analyzing repository practices.

### self-hosted-container.yml

**Description:** Demonstrates running workflows on self-hosted runners with container support.

**Trigger Events:** Manual trigger via `workflow_dispatch`.

**Jobs:**
- **externals:** Checks external directories on a self-hosted runner.
- **externals-container:** Runs checks within a container on a self-hosted runner.
- **test-with-job-container:** Demonstrates job execution within a container on a self-hosted runner.
- **test-with-services:** Demonstrates using services with self-hosted runners.

**Special Notes:** Showcases the capabilities and configurations of self-hosted runners with containers.

### self-hosted.yml

**Description:** A simple workflow demonstrating the use of self-hosted runners.

**Trigger Events:** Manual trigger via `workflow_dispatch`.

**Jobs:**
- **job1:** Executes a sleep command on a self-hosted runner.

**Special Notes:** Useful for testing and demonstrating self-hosted runner configurations.

### workflow-metrics.yml

**Description:** Collects and analyzes metrics for workflow runs within the repository.

**Trigger Events:** Manual trigger via `workflow_dispatch`.

**Jobs:**
- **evaluate-actions-consumption:** Collects metrics on workflow runs and outputs analysis.

**Special Notes:** Provides insights into workflow efficiency and resource consumption.

### workflow-with-protection-check.yml

**Description:** Checks if the selected environment for deployment is protected before proceeding.

**Trigger Events:** Manual trigger via `workflow_dispatch` with environment selection.

**Jobs:**
- **check:** Determines if the selected environment is protected.
- **deploy:** Proceeds with deployment if the environment is protected.

**Special Notes:** Ensures deployments are made to protected environments, enhancing security.
