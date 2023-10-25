# GitHub Workflow for Maven

GitHub workflow to build and publish Maven projects, then invoke a webhook.


### Workflow usage example:
```yml
name: Validate and optionally publish (if pushed on main)

on:
  push:

jobs:
  build-and-publish:
    uses: mekomsolutions/mekom-github-workflow-maven/.github/workflows/build-publish-workflow.yml@main
    with:
      webhook-url: https://openmrs-cd.mekomsolutions.net/generic-webhook-trigger/invoke
      java-version: '8' # Optional, defaults to Java 8
    secrets:
      NEXUS_USERNAME: ${{ secrets.NEXUS_USERNAME }}
      NEXUS_PASSWORD: ${{ secrets.NEXUS_PASSWORD }}
      OCD3_USERNAME: ${{ secrets.OCD3_USERNAME }}
      OCD3_PASSWORD: ${{ secrets.OCD3_PASSWORD }}
    if: ${{ github.ref == 'refs/heads/main' }}
```

The publishing relies on the `<distributionManagement>` block to be configured in the Maven project being built.
At the moment, only a specific list of server IDs is supported. See [the list of supported server IDs](.github/workflows/build-publish-workflow.yml#L44-L73)

List of inputs:
```
    maven-args:
      required: false
      type: string
    webhook-url:
      required: true
      type: string
    java-version:
      required: false
      type: string
      default: '8'
    secrets:
      NEXUS_USERNAME:
        required: true
      NEXUS_PASSWORD:
        required: true
      OCD3_USERNAME:
        required: true
      OCD3_PASSWORD:
        required: true
```
