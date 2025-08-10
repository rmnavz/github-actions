# Publish Package (NuGet Push Only)

Publishes NuGet packages to a specified NuGet or package source. No GitHub release is created. Designed for universal use and workflow reusability.

## Inputs

| Name            | Type    | Required | Default                           | Description                                      |
|-----------------|---------|----------|-----------------------------------|--------------------------------------------------|
| artifact_name   | string  | Yes      |                                   | Name of the NuGet artifact to download           |
| package_pattern | string  | No       | **/*.nupkg                        | Glob pattern for .nupkg files to publish         |
| nuget_source    | string  | No       | <https://api.nuget.org/v3/index.json> | NuGet/package source URL                        |

## Secrets

| Name          | Required | Description                                 |
|---------------|----------|---------------------------------------------|
| NUGET_API_KEY | Yes      | API key for publishing to the NuGet/package source |

## Usage Example

```yaml
jobs:
  publish-nuget-push:
    uses: rmnavz/github-actions/.github/workflows/publish-package-nuget-push.yml@v1.0.0
    with:
      artifact_name: 'nuget-packages'
      package_pattern: '**/*.nupkg'
      nuget_source: 'https://api.nuget.org/v3/index.json'
    secrets:
      NUGET_API_KEY: ${{ secrets.NUGET_API_KEY }}
```

## Description

This workflow downloads a specified artifact containing NuGet packages, then publishes all matching `.nupkg` files to the specified NuGet or package source. It is suitable for both public and private feeds. No GitHub release is created.

## Steps

1. **Setup .NET**: Installs the required .NET SDK version.
2. **Checkout Source Code**: Checks out the repository.
3. **Download NuGet Packages**: Downloads the specified artifact containing `.nupkg` files.
4. **Fail if no packages found**: Fails the workflow if no matching `.nupkg` files are found.
5. **Publish to NuGet**: Pushes each `.nupkg` file to the specified NuGet/package source using the provided API key.

## Outputs

| Name | Description |
|------|-------------|
| (none) | This workflow does not produce outputs. |

## Requirements

- Required: GitHub Actions runner with internet access
- Required: Valid NuGet API key for the target source
- Optional: Private NuGet feed URL if publishing to a private source

## Related Workflows

- [publish-package-nuget-release](publish-package-nuget-release.md): Publishes NuGet packages and creates a GitHub release
- [build-package-dotnet-ci](build-package-dotnet-ci.md): Builds .NET packages for publishing

## Contributing

Contributions are welcome! Please open issues or pull requests for improvements, bug fixes, or new features. See the repository guidelines for more information.

## Notes

- The `package_pattern` input allows you to control which packages are published (e.g., a specific file or all in a directory).
- The `nuget_source` input can be set to a private feed URL if needed.
- The workflow uses `--skip-duplicate` to avoid errors if a package version already exists.
