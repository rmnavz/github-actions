# Version (Semantic, Generic CI) Workflow Documentation

This document describes the `version-semver-generic-ci.yml` reusable workflow for determining a semantic version using GitVersion in a language-agnostic way. This workflow is intended for use in CI pipelines where you need to calculate and output a semantic version for use by other workflows or jobs, without creating or pushing tags.

## Purpose

- Calculate a semantic version using [GitVersion](https://gitversion.net/).
- Output version information (semver, major, minor, patch, fullSemVer) for use in downstream workflows.
- Designed for maximum reusability and language independence.

## Usage Example

```yaml
jobs:
  get-version:
    uses: rmnavz/github-actions/.github/workflows/version-semver-generic-ci.yml@v1.0.0
    with:
      gitversion_version: '5.x'
      gitversion_config: '.github/gitversion.yml'
```

## Inputs

| Name               | Type    | Required | Default | Description                                      |
|--------------------|---------|----------|---------|--------------------------------------------------|
| gitversion_version | string  | No       | 5.x     | GitVersion version to use                        |
| gitversion_config  | string  | No       |         | Path to gitversion.yml config file (optional)    |

## Outputs

| Name        | Description                |
|-------------|---------------------------|
| semver      | The calculated semver      |
| major       | Major version              |
| minor       | Minor version              |
| patch       | Patch version              |
| fullSemVer  | Full semantic version      |

## Steps Overview

1. **Checkout Source Code**: Fetches the repository with full history.
2. **Install GitVersion**: Installs the specified version of GitVersion.
3. **Determine Semantic Version**: Runs GitVersion and extracts version info.
4. **Debug Output**: Prints the version.json and extracted semver for troubleshooting.

## Best Practices

- Use this workflow as a reusable building block for versioning in CI/CD.
- Pin the workflow version and all action versions for reproducibility.
- Pass the outputs to downstream jobs or workflows as needed.

## Related Links

- [GitVersion Documentation](https://gitversion.net/)
- [GitHub Actions Reusable Workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows)

---

## Last updated: 2025-08-08
