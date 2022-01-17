<p align="center">
  <a href="https://github.com/crs-k/release-draft/actions"><img alt="ci status" src="https://github.com/crs-k/release-draft/actions/workflows/ci.yml/badge.svg"></a>
  <a href="https://github.com/crs-k/release-draft/actions"><img alt="ci status" src="https://github.com/crs-k/release-draft/actions/workflows/codeql-analysis.yml/badge.svg"></a>
</p>

# Release Draft Create & Update

This Action automatically creates and/or updates release drafts.
* Generates & updates release notes. More info [here](https://docs.github.com/en/repositories/releasing-projects-on-github/automatically-generated-release-notes).
* Draft tag defaults to previous semver compliant tag +1 patch.

## Usage

### Pre-requisites
Create a workflow `.yml` file in your repository's `.github/workflows` directory. An [example workflow](#example-workflow) is available below. For more information, reference the GitHub Help Documentation for [Creating a workflow file](https://help.github.com/en/articles/configuring-a-workflow#creating-a-workflow-file).

### Inputs

* `repo-token` - The GITHUB_TOKEN secret. 
* `commitish` - Release target. Default: `main` branch.
* `bump` - NOT AVAILABLE. Semver bump type. Options: major, minor, patch, prerelease. Default: patch.

### Outputs

* `id` - The ID of the created Release.
* `html_url` - The URL users can navigate to in order to view the release.
* `upload_url` - The URL for uploading assets to the release.

### Example workflow

```yaml
name: Release Draft

on:
  workflow_dispatch:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
  release:
      types: [published]

jobs:
  release_draft:
    runs-on: ubuntu-latest
    steps:
    - name: Release Draft
      uses: crs-k/release-draft@v0.3.3
      with:
        repo-token: "${{ secrets.GITHUB_TOKEN }}"
```

