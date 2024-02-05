# Docker Build and Publish Workflow

This workflow is named `Docker Build and Publish`. It is designed to build and publish Docker images.

## Workflow Triggers

This workflow is triggered when it is called from another workflow.

## Inputs

- `context`: Path to the build context. Default is `.`.
- `dockerfile`: Path to the Dockerfile to build. Default is `Dockerfile`.
- `image-name`: Name of the image to build. This is a required input.

## Secrets

- `DOCKER_HUB_USERNAME`: Required for the workflow.
- `DOCKER_HUB_PASSWORD`: Required for the workflow.

## Jobs

1. `build-publish`: Builds and publishes the Docker image. The image is tagged with `latest` and the version from the Maven project. The image is built for `linux/amd64` and `linux/arm64` platforms.

## Usage

This workflow is designed to be called from another workflow. It is not intended to be used on its own.

```yaml
name: Docker Build and Publish

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
  release:
    types: [published]

jobs:
  build-publish:
    uses: mekomsolutions/shared-github-workflow/.github/workflows/docker-build-publish.yml@main
    with:
      context: . # Optional default value: .
      dockerfile: Dockerfile # Optional default value: Dockerfile
      image-name: my-image # Required
    secrets:
      DOCKER_HUB_USERNAME: ${{ secrets.DOCKER_HUB_USERNAME }}
      DOCKER_HUB_PASSWORD: ${{ secrets.DOCKER_HUB_PASSWORD }}
```

Replace `my-image` with the name of the Docker image you want to build and publish. You also need to set the `DOCKER_HUB_USERNAME` and `DOCKER_HUB_PASSWORD` secrets in your repository settings.

For more information about reusable workflows, see the official GitHub documentation: [https://docs.github.com/en/actions/using-workflows/reusing-workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows).
