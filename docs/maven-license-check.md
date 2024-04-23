# Maven License Check Workflow

This workflow is named `Maven License Check`. It is designed to check the code licensing of a Maven project using the License Maven Plugin.

## Workflow Triggers

This workflow is triggered when it is called from another workflow.

## Inputs

- `java-version`: Java version to use for building. Default is `17`.
- `java-distribution`: Java distribution to use for building. Default is `temurin`.
- `maven-args`: Additional arguments to pass to the Maven command. Default to empty.

## Jobs

1. `check`: Checks the code licensing using the License Maven Plugin.

## Usage

This workflow is designed to be used as part of the CI/CD pipeline. It is triggered automatically on every push and pull request.

```yaml
name: Maven License Check

on:
  push: [main]
  pull_request: [main]

jobs:
    check:
      uses: mekomsolutions/shared-github-workflow/.github/workflows/maven-license-check.yml@main
      with:
        java-version: 17 # Optional, default is 17
        java-distribution: temurin # Optional, default is temurin
        maven-args: '' # Optional, default is empty
```

For more information about reusable workflows, see the official GitHub documentation: [https://docs.github.com/en/actions/using-workflows/reusing-workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows).
