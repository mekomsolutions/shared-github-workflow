# Maven Spotless Check Workflow

This workflow is named `Maven Spotless Check`. It is designed to check the code formatting of a Maven project using the Spotless plugin.

## Workflow Triggers

This workflow is triggered when it is called from another workflow.

## Inputs

- `java-version`: Java version to use for building. Default is `17`.
- `java-distribution`: Java distribution to use for building. Default is `temurin`.

## Jobs

1. `spotless-check`: Checks the code formatting using the Spotless plugin.

## Usage

This workflow is designed to be used as part of the CI/CD pipeline. It is triggered automatically on every push and pull request.

```yaml
name: Maven Spotless Check

on:
  push: [main]
  pull_request: [main]

jobs:
  spotless-check:
    uses: mekomsolutions/shared-github-workflow/.github/workflows/maven-spotless-check.yml@main
```

For more information about reusable workflows, see the official GitHub documentation: [https://docs.github.com/en/actions/using-workflows/reusing-workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows).
