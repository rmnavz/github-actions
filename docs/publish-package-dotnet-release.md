# Publish Package (.NET Release) Workflow

This workflow publishes NuGet packages and creates a GitHub release. Designed for universal use and workflow reusability.

## Purpose

- Publish NuGet packages to NuGet.org
- Create a GitHub release with release notes

## Inputs

| Name                 | Type     | Required | Default         | Description                                 |
|----------------------|----------|----------|-----------------|---------------------------------------------|
| release_version      | string   | Yes      |                 | Release version (e.g., 1.2.3, 2025.08.08)   |
| prerelease           | boolean  | No       | false           | Is this a prerelease?                       |
| include_test_results | boolean  | No       | true            | Include test results in release notes       |
| artifact_name        | string   | No       | nuget-packages  | Name of the NuGet artifact to download      |

## Secrets

| Name           | Description                                 |
|----------------|---------------------------------------------|
| NUGET_API_KEY  | API key for publishing to NuGet.org         |
| GITHUB_TOKEN   | GitHub token for creating releases          |

## Outputs

| Name         | Type   | Description                        |
|--------------|--------|------------------------------------|
| release_url  | string | URL of the created GitHub release   |

## Example Usage

```yaml
jobs:
  publish:
    uses: rmnavz/github-actions/.github/workflows/publish-package-dotnet-release.yml@v1.0.0
    with:
      release_version: '1.2.3'
    secrets:
      NUGET_API_KEY: ${{ secrets.NUGET_API_KEY }}
      GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## Best Practices

- Use strong secrets management for API keys.
- Include test results in release notes for transparency.
- Use tags for stable workflow references.
