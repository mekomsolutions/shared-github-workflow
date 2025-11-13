# Maven Integration Test Workflow

It is designed to clone and run integration tests repository in a Maven build.

## Workflow Triggers

This workflow is triggered when it is called from another workflow.

## Inputs

- `maven-args`: Additional arguments to pass to Maven. Default is `-DskipTests=false`.
- `maven-phase`: The Maven phase to run. Default is `verify`.
- `java-version`: Java version to use for building. Default is `17`.
- `java-distribution`: Java distribution to use for building. Default is `temurin`.
- `use-secrets`: Whether to use secrets for Maven registry authentication. Default is `false`. If `true`, the secrets
  `MAVEN_USERNAME` and `MAVEN_PASSWORD` must be set.
- `integration-tests-repo`: The integration test repo to clone.
- `integration-tests-branch`: The branch to checkout in the integration test repo.
- `integration-tests-path`: The path where the integration test repo is checked out.

## Usage

Below is an example of how to call this workflow from another workflow:

```yaml
name: Run Integration Tests

on:
  push: [ main ]
  pull_request: [ main ]

jobs:
  integration-test:
    uses: mekomsolutions/shared-github-workflow/.github/workflows/maven-integration-test.yml@main
    with:
      maven-args: "-DskipTests=false"
      maven-phase: "verify"
      java-version: "17"
      java-distribution: "temurin"
      use-secrets: "false"
      integration-tests-repo: "ozone-his/ozone-it"
      integration-tests-branch: "main"

```

For more information about reusable workflows, see the official GitHub
documentation: [https://docs.github.com/en/actions/using-workflows/reusing-workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows).
