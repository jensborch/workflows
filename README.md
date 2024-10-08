[![Lint](https://github.com/jensborch/workflows/actions/workflows/action-lint.yml/badge.svg)](https://github.com/jensborch/workflows/actions/workflows/action-lint.yml)

# Reusable workflows

Reusable Github workflows for Gradle, Maven, Code scanning, Dependabot etc..

## dependabot-automerge.yml

```yml
name: "Dependabot Automerge"

on:
  pull_request:
    branches: [ master ]

jobs:
  automerge:
    uses: jensborch/workflows/.github/workflows/dependabot-automerge.yml.yml@main
    permissions:
      pull-requests: write
      contents: write    
    secrets: inherit
```

### Inputs, variables and secrets

* vars.AUTOMERGE_APP_ID
* secrets.AUTOMERGE_APP_PRIVATE_KEY
* secrets.GITHUB_TOKEN

## gradle-build.yml

```yml
name: Build

on:
  push:
  workflow_dispatch:

jobs:
  build:
    uses: jensborch/workflows/.github/workflows/gradle-build.yml@main
    with:
        java-version: 8
```

### Inputs, variables and secrets

* inputs.java-version

## gradle-publish.yml

```yml
name: Publish

on:
  push:
    branches: [master]

jobs:
  publish:
    uses: jensborch/workflows/.github/workflows/gradle-publish.yml@main
    secrets: inherit
    permissions:
      contents: write
    with:
        java-version: 8
```

### Inputs, variables and secrets

* inputs.java-version
* secrets.GITHUB_TOKEN
* secrets.SONATYPE_USERNAME
* secrets.SONATYPE_PASSWORD
* secrets.SIGNING_KEY
* secrets.SIGNING_PASSWORD

## gradle-release.yml

```yml
name: Release

on:
  push:
    branches:
      - 'releases/**'

jobs:
  release:
    uses: jensborch/workflows/.github/workflows/gradle-release.yml@main
    secrets: inherit
    permissions:
      contents: write
      pull-requests: write
    with:
        java-version: 8
```

### Inputs, variables and secrets

* inputs.java-version
* vars.RELEASE_APP_ID
* secrets.RELEASE_APP_PRIVATE_KEY

## maven-build.yml

```yml
name: Build

on:
  push:
  workflow_dispatch:  

jobs:
  build:
    uses: jensborch/workflows/.github/workflows/maven-build.yml@main
    secrets: inherit
    with:
        java-version: 11
```

## maven-publish.yml

```yml
name: Build

on:
  push:
    branches: [master]

jobs:
  build:
    uses: jensborch/workflows/.github/workflows/maven-build.yml@main
    secrets: inherit
    with:
        java-version: 11
```

## maven-publish.yml

```yml
name: Publish

on:
  push:

jobs:
  build:
    uses: jensborch/workflows/.github/workflows/maven-publish.yml@main
    secrets: inherit
    permissions:
      contents: write
    with:
        java-version: 11
```

### Inputs, variables and secrets

* secrets.SONATYPE_USERNAME
* secrets.SONATYPE_PASSWORD
* secrets.SIGNING_PASSWORD

## maven-release.yml

```yml
name: Release

on:
  push:

jobs:
  build:
    uses: jensborch/workflows/.github/workflows/maven-release.yml@main
    secrets: inherit
    permissions:
      contents: write
      pull-requests: write
    with:
        java-version: 11
```

### Inputs, variables and secrets

* inputs.java-version
* vars.RELEASE_APP_ID
* secrets.RELEASE_APP_PRIVATE_KEY
