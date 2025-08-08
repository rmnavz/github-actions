# Build Package (.NET CI) Workflow

This workflow builds and packages a .NET project, uploading NuGet packages as artifacts. Designed for universal use and workflow reusability.

## Purpose

- Build and package .NET projects
- Upload NuGet packages as artifacts

## Inputs

| Name                   | Type     | Required | Default         | Description                                 |
|------------------------|----------|----------|-----------------|---------------------------------------------|
| release_version        | string   | Yes      |                 | Release version (e.g., 1.2.3, 2025.08.08)   |
| dotnet_version         | string   | No       | 8.0.x           | .NET SDK version to use                     |
| project_path           | string   | No       | .               | Path to solution/project                    |
| artifact_name          | string   | No       | nuget-packages  | Name for uploaded artifact                  |
| artifact_paths         | string   | No       | ./artifacts/*.nupkg | Paths to include in artifact            |
| artifact_retention_days| number   | No       | 7               | Days to keep artifact                       |
| upload_artifacts       | boolean  | No       | true            | Whether to upload build artifacts           |

## Outputs

| Name           | Type     | Description                        |
|----------------|----------|------------------------------------|
| nuget_packages | artifact | The produced NuGet package files    |

## Example Usage

```yaml
jobs:
  build-package:
    uses: rmnavz/github-actions/.github/workflows/build-package-dotnet-ci.yml@v1.0.0
    with:
      release_version: '1.2.3'
```

## Best Practices

- Use semantic versioning for releases.
- Upload artifacts for traceability and distribution.
