# Shared GitHub Workflows

This repository contains shared GitHub workflows that can be used in other repositories.
 
## Workflows

The following workflows are available in this repository:

- [Docker Build and Publish](docs/docker-build-publish.md)
- [Maven Build and Test](docs/maven-build-test.md)
- [Maven Spotless Check](docs/maven-spotless-check.md)
- [Notify OCD3](docs/ocd3-notify.md)
- [Maven Check Dependency Changes ](docs/maven-check-deps-build-publish.md)

## Usage

To use a workflow in your repository, create a new workflow file in the `.github/workflows` directory of your repository and use the `uses` keyword to include the workflow from this repository.

For example, to use the `Docker Build and Publish` workflow, create a new file `.github/workflows/docker-build-publish.yml` in your repository with the following content:

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

## Contributing

To contribute a new workflow or make changes to an existing workflow, create a pull request with your changes. The pull request will be reviewed and merged by the repository maintainers.
