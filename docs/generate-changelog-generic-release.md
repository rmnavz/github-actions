# Generate Changelog (Generic Release) Workflow

> **Reusable workflow for generating and optionally committing a changelog using [conventional-changelog-cli](https://github.com/conventional-changelog/conventional-changelog).**

---

## Overview

This workflow automates changelog generation for your repository using a configurable preset and options.  
It can be used as a reusable workflow via `workflow_call` in other repositories.

---

## Features

- Generates a changelog file based on commit history and a conventional changelog preset.
- Optionally commits and pushes changelog updates.
- Supports custom changelog file paths, release counts, and tag-specific changelogs.
- Uploads the changelog as a workflow artifact.
- Provides a summary in the workflow run.

---

## Inputs

| Name               | Type    | Default         | Description                                                                 |
|--------------------|---------|-----------------|-----------------------------------------------------------------------------|
| `node_version`     | string  | `20`            | Node.js version for changelog tooling                                       |
| `changelog_preset` | string  | `angular`       | Conventional changelog preset (angular, atom, etc.)                         |
| `changelog_file`   | string  | `CHANGELOG.md`  | Path to changelog file                                                      |
| `commit_changelog` | boolean | `true`          | Automatically commit and push changelog updates                             |
| `tag_name`         | string  | `""`            | Git tag name for release-specific changelog (optional)                      |
| `release_count`    | number  | `-1`            | Number of releases to include in changelog (`-1` = all)                     |
| `skip_ci`          | boolean | `true`          | Add `[skip ci]` to commit message                                           |

---

## Outputs

| Name               | Description                                 |
|--------------------|---------------------------------------------|
| `changelog_updated`| Whether changelog was updated (`true/false`)|
| `changelog_path`   | Path to the updated changelog file          |

---

## Usage Example

```yaml
name: Generate Changelog

on:
  workflow_dispatch:

jobs:
  changelog:
    uses: your-org/github-actions/.github/workflows/generate-changelog-generic-release.yml@main
    with:
      changelog_preset: 'angular'
      changelog_file: 'CHANGELOG.md'
      commit_changelog: true
      tag_name: ''
      release_count: -1
      skip_ci: true
```

---

## Best Practices

- Use this workflow after merging PRs or before releases to keep your changelog up to date.
- Adjust `changelog_preset` to match your commit style.
- Set `commit_changelog: false` if you want to review changes before committing.
- Use `tag_name` for generating changelogs for specific releases.

---

## Related Workflows

- [Tag Git (Generic Release)](tag-git-generic-release.md)
- [Build Package (.NET CI)](build-package-dotnet-ci.md)

---

## References

- [conventional-changelog-cli](https://github.com/conventional-changelog/conventional-changelog)
- [GitHub Actions: Reusable Workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows)

---
