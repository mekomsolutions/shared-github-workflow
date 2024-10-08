# Check for Dependency Changes Workflow

This workflow is named `Check for dependency changes`. It is designed to check for changes in the dependencies of a Maven project and build the project if changes are detected. It also publishes the build to Nexus using a shared GitHub workflow. Optionally, it can upload the artifacts to GitHub using the `upload-artifacts` action.

## Workflow Triggers

This workflow is triggered when it is called from another workflow.

## Inputs

- `maven-args`: Additional arguments to pass to Maven. Default is `-DskipTests=true`.
- `java-version`: Java version to use for building. Default is `17`.
- `java-distribution`: Java distribution to use for building. Default is `temurin`.
- `upload-artifacts`: Whether to upload the artifacts to GitHub using upload-artifacts action. Default is `false`.
- `upload-artifacts-path`: The path to the artifacts to upload. Default is empty.
- `upload-artifacts-name`: The name of the artifacts to upload. Default is `artifact`.
- `notify-ocd3`: Whether to notify the OCD3 about the new published artifacts. Default is `false`.
- `ocd3-webhook-url`: The Webhook URL of the OCD3 to notify. Default is `https://openmrs-cd.mekomsolutions.net/generic-webhook-trigger/invoke`.
- `check-deps-timeout-minutes`: The timeout in minutes for the check-for-dependency-changes job. Default is `10`.
- `check-deps-maven-args`: Additional arguments to pass to the Maven command in the check-for-dependency-changes job. Default is empty.

## Secrets

- `NEXUS_USERNAME`: Required for the workflow.
- `NEXUS_PASSWORD`: Required for the workflow.
- `OCD3_USERNAME`: Optional.
- `OCD3_PASSWORD`: Optional.

## Jobs

1. `check-for-dependency-changes`: Checks for changes in the dependencies of the Maven project.
2. `build`: Builds the project if changes in dependencies are detected.
3. `publish`: Publishes the build using a shared GitHub workflow.

## Usage

This workflow is designed to be called from another workflow. It is not intended to be used on its own.

```yaml
name: Check for dependency changes

on:
  workflow_dispatch:
  schedule:
    - cron: '10 */12 * * *' # every 12 hours

jobs:
  check-deps:
    uses: mekomsolutions/shared-github-workflow/.github/workflows/maven-check-deps-build-publish.yml@main
    with:
      maven-args: -DskipTests=true # Optional, default is -DskipTests=true
      java-version: 17 # Optional, default is 17
      java-distribution: temurin # Optional, default is temurin
      upload-artifacts: false # Optional, default is false
      upload-artifacts-path: '' # Optional, default is empty
      upload-artifacts-name: artifact # Optional, default is artifact
      notify-ocd3: false # Optional, default is false
      ocd3-webhook-url: https://openmrs-cd.mekomsolutions.net/generic-webhook-trigger/invoke # Optional
    secrets:
      NEXUS_USERNAME: ${{ secrets.NEXUS_USERNAME }}
      NEXUS_PASSWORD: ${{ secrets.NEXUS_PASSWORD }}
      OCD3_USERNAME: ${{ secrets.OCD3_USERNAME }} # Optional
      OCD3_PASSWORD: ${{ secrets.OCD3_PASSWORD }} # Optional
```

Replace `NEXUS_USERNAME` and `NEXUS_PASSWORD` with the credentials to access the Maven repository. You also need to set the `NEXUS_USERNAME` and `NEXUS_PASSWORD` secrets in your repository settings.

For more information about reusable workflows, see the official GitHub documentation: [https://docs.github.com/en/actions/using-workflows/reusing-workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows).
