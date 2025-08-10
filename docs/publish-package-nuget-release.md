# Publish Package (NuGet Release)

Publishes NuGet packages to nuget.org and optionally creates a GitHub release with attached packages and release notes.

## 📝 Purpose

- Automate NuGet package publishing and release creation for any versioning scheme
- Attach published packages to the GitHub release
- Generate release notes with changelog and recent commits

## 🚦 Triggers

- `workflow_call` (for reuse in other repos)
- `workflow_dispatch` (manual trigger)

## 🔗 Inputs

| Name                | Type      | Required | Default        | Description                                             |
|---------------------|-----------|----------|----------------|---------------------------------------------------------|
| release_version     | string    | yes      |                | Release version (e.g., v1.0, 2025.08.10, release-42)    |
| artifact_name       | string    | yes      |                | Name of the NuGet artifact to download                  |
| changelog_path      | string    | no       | CHANGELOG.md   | Path to changelog file                                  |
| commit_count        | number    | no       | 10             | Number of recent commits to include                      |
| create_github_release| boolean  | no       | true           | Whether to create a GitHub release                      |

## 🔒 Secrets

| Name         | Required | Description                        |
|--------------|----------|------------------------------------|
| NUGET_API_KEY| yes      | API key for publishing to NuGet.org |
| GITHUB_TOKEN | no       | GitHub token for creating releases  |

## 📤 Outputs

| Name        | Description                      |
|-------------|----------------------------------|
| release_url | URL of the created GitHub release|

## 🚀 Example Usage

```yaml
jobs:
  publish-nuget-release:
    uses: rmnavz/github-actions/.github/workflows/publish-package-nuget-release.yml@v1.0.0
    with:
      release_version: 'v1.0.0'
      artifact_name: 'nuget-packages'
      create_github_release: true
    secrets:
      NUGET_API_KEY: ${{ secrets.NUGET_API_KEY }}
      GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

## 🏆 Best Practices

- Use a consistent artifact name for NuGet packages (e.g., `nuget-packages`)
- Ensure `.nupkg` files are present in the artifact root
- Use a specific tag (e.g., `@v1.0.0`) when referencing this workflow
- Document all workflow parameters in your repository for clarity

## 🔗 Related Workflows

- [Publish Release (Generic Release)](publish-release-generic-release.md)

---

For more details, see the main [README](../README.md).
