# Maven Build and Test Workflow

This workflow is named `Maven Build and Test`. It is designed to build and test a Maven project. 

## Workflow Triggers

The workflow is triggered when it is called from another workflow.

## Inputs

- `maven-args`: Additional arguments to pass to Maven. Default is `-DskipTests=false`.
- `java-version`: Java version to use for building. Default is `17`.
- `java-distribution`: Java distribution to use for building. Default is `temurin`.

## Jobs

1. `build-test`: Builds the project and runs the tests.

## Usage

This workflow is designed to be used as part of the CI/CD pipeline. It is triggered automatically on every push and pull request.

```yaml
name: Maven Build and Test

on:
  push: [main]
  pull_request: [main]

jobs:
  build-test:
    uses: mekomsolutions/shared-github-workflow/.github/workflows/maven-build-test.yml@main
    with:
      maven-args: -DskipTests=false # Optional default value: -DskipTests=false
      java-version: 17 # Optional default value: 17
      java-distribution: temurin # Optional default value: temurin
    secrets:
      NEXUS_USERNAME: ${{ secrets.NEXUS_USERNAME }}
      NEXUS_PASSWORD: ${{ secrets.NEXUS_PASSWORD }}
```

Replace `NEXUS_USERNAME` and `NEXUS_PASSWORD` with the credentials to access the Maven repository. You also need to set the `NEXUS_USERNAME` and `NEXUS_PASSWORD` secrets in your repository settings.

For more information about reusable workflows, see the official GitHub documentation: [https://docs.github.com/en/actions/using-workflows/reusing-workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows).
