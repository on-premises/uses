## About
A shared-workflow for various tasks for [@on-premises](https://github.com/on-premises).

## Example
Here is an example of how to use this workflow in your repository. It can be used in other workflows by calling it with the appropriate inputs.

### `.github/workflows/use-docker.yml`
```yaml
name: Docker

on:
  workflow_dispatch:
  push:
    branches:
      - main
      - develop
  pull_request:
    types: [opened, synchronize, reopened]

concurrency:
  group: ${{ github.workflow }}-${{ github.ref }}
  cancel-in-progress: true

jobs:
  docker:
    uses: on-premises/workflows/.github/workflows/use-docker.yml@main
    permissions:
      contents: read
      packages: write
    with:
      push: ${{ github.event_name != 'pull_request' }}
```
