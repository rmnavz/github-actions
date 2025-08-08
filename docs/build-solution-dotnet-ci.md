# Build Solution (.NET CI) Workflow

This workflow builds a .NET solution or project, caches dependencies, and optionally uploads build artifacts. It is designed for universal use via `workflow_call` in other repositories.

## Purpose

- Build .NET solutions or projects
- Cache NuGet packages and build outputs
- Upload build artifacts for downstream jobs

## Inputs

| Name                   | Type     | Required | Default      | Description                                 |
|------------------------|----------|----------|--------------|---------------------------------------------|
| dotnet_version         | string   | No       | 8.0.x        | .NET SDK version to use                     |
| project_path           | string   | No       | ""           | Path to solution/project (blank = auto)     |
| artifact_name          | string   | No       | build-artifacts | Name for uploaded artifact                  |
| artifact_paths         | string   | No       | **/bin/Release/ | Paths to include in artifact                |
| artifact_retention_days| number   | No       | 7            | Days to keep artifact                       |
| upload_artifacts       | boolean  | No       | true         | Whether to upload build artifacts           |

## Outputs

| Name         | Type   | Description                        |
|--------------|--------|------------------------------------|
| build_status | string | Status of the build job            |
| artifact_url | string | URL of the uploaded artifact        |

## Example Usage

```yaml
jobs:
  build:
    uses: rmnavz/github-actions/.github/workflows/build-solution-dotnet-ci.yml@v1.0.0
    with:
      dotnet_version: '8.0.x'
      project_path: 'src/MyApp.sln'
```

## Best Practices

- Use specific tags (e.g., `@v1.0.0`) when referencing this workflow.
- Keep build jobs focused and modular.
- Document all inputs and outputs in your calling workflow.
