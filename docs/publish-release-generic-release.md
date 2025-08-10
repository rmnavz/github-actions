# Publish Release (Generic Release)

Creates a GitHub release with any versioning scheme, attaches specified artifacts, and generates release notes. This workflow is designed for universal use and can be called from any repository.

## 📝 Purpose

- Automate GitHub release creation for any versioning scheme (not just semver)
- Attach any set of build artifacts to the release
- Generate release notes with changelog, recent commits, and (optionally) test results

## 🚦 Triggers

- `workflow_call` (for reuse in other repos)
- `workflow_dispatch` (manual trigger)

## 🔗 Inputs

| Name                | Type      | Required | Default        | Description                                             |
|---------------------|-----------|----------|----------------|---------------------------------------------------------|
| release_version     | string    | yes      |                | Release version (e.g., v1.0, 2025.08.10, release-42)    |
| artifact_names      | string    | yes      |                | Comma-separated list of artifact names to attach         |
| include_test_results| boolean   | no       | false          | Include test results in release notes                    |
| changelog_path      | string    | no       | CHANGELOG.md   | Path to changelog file                                  |
| commit_count        | number    | no       | 10             | Number of recent commits to include                      |

## 🔒 Secrets

| Name         | Required | Description                        |
|--------------|----------|------------------------------------|
| GITHUB_TOKEN | yes      | GitHub token for creating releases |

## 📤 Outputs

| Name        | Description                      |
|-------------|----------------------------------|
| release_url | URL of the created GitHub release|

## 🚀 Example Usage

```yaml
jobs:
  publish-release:
    uses: rmnavz/github-actions/.github/workflows/publish-release-generic-release.yml@v1.0.0
    with:
      release_version: 'v1.0.0'
      artifact_names: 'nuget-packages,docs-artifact'
      include_test_results: false
      changelog_path: 'CHANGELOG.md'
      commit_count: 10
```

## 🏆 Best Practices

- Use descriptive artifact names and ensure they are uploaded in previous jobs.
- Keep changelog up to date for meaningful release notes.
- Use a specific tag (e.g., `@v1.0.0`) when referencing this workflow.
- Document all workflow parameters in your repository for clarity.

## 🔗 Related Workflows

- [Publish Package (.NET Release)](publish-package-dotnet-release.md)
- [Tag Git (Generic Release)](tag-git-generic-release.md)

---

For more details, see the main [README](../README.md).
