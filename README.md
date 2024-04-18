[![Lint](https://github.com/jensborch/workflows/actions/workflows/action-lint.yml/badge.svg)](https://github.com/jensborch/workflows/actions/workflows/action-lint.yml)

# Reusable workflows

Reusable Github workflows for Gradle, Maven, Code scanning, Dependabot etc..

## codeql-analysis.yml

```yml
name: 'Code Scanning - Action'

on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
  schedule:
    #        ┌───────────── minute (0 - 59)
    #        │  ┌───────────── hour (0 - 23)
    #        │  │ ┌───────────── day of the month (1 - 31)
    #        │  │ │ ┌───────────── month (1 - 12 or JAN-DEC)
    #        │  │ │ │ ┌───────────── day of the week (0 - 6 or SUN-SAT)
    #        │  │ │ │ │
    #        │  │ │ │ │
    #        │  │ │ │ │
    #        *  * * * *
    - cron: '30 1 * * 0'

jobs:
  scan:
    uses: jensborch/workflows/.github/workflows/codeql-analysis.yml.yml@main
```

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
    branches: [ master ]
  pull_request:
    types: [opened, reopened]

jobs:
  build:
    uses: jensborch/workflows/.github/workflows/gradle-build.yml@main
    secrets: inherit
    with:
        java-version: 8
```

### Inputs, variables and secrets

* inputs.java-version

## gradle-publish.yml

```yml
name: Publish

on:
  pull_request:
    branches: [master]
    types: [closed]

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

### gradle-release.yml

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
    with:
        java-version: 8
```

* inputs.java-version
* vars.RELEASE_APP_ID
* secrets.RELEASE_APP_PRIVATE_KEY

## maven-build.yml

```yml
name: Build

on:
  push:
    branches: [ master ]
  pull_request:
    types: [opened, reopened]

jobs:
  build:
    uses: jensborch/workflows/.github/workflows/maven-build.yml@main
    secrets: inherit
    with:
        java-version: 11
```
