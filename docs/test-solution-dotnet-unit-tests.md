# Test Solution (.NET Unit Tests) Workflow

This workflow runs tests for a .NET solution or project, collects code coverage, and uploads test results as artifacts. Designed for universal use via `workflow_call`.

## Purpose

- Run .NET unit tests
- Collect code coverage
- Upload test results for reporting

## Inputs

| Name                     | Type     | Required | Default      | Description                                 |
|--------------------------|----------|----------|--------------|---------------------------------------------|
| dotnet_version           | string   | No       | 8.0.x        | .NET SDK version to use                     |
| project_path             | string   | No       | ""           | Path to solution/project (blank = auto)     |
| use_build_artifact       | boolean  | No       | false        | Use build artifact from previous job        |
| build_artifact_name      | string   | No       | build-artifacts | Name of build artifact to download         |
| test_results_artifact_name| string  | No       | test-results | Name for uploaded test results artifact     |
| test_results_paths       | string   | No       | TestResults/**/*.trx, TestResults/**/*.xml | Paths to test result files                  |
| test_results_retention_days| number | No       | 30           | Days to keep test results artifact          |

## Example Usage

```yaml
jobs:
  test:
    uses: rmnavz/github-actions/.github/workflows/test-solution-dotnet-unit-tests.yml@v1.0.0
    with:
      dotnet_version: '8.0.x'
      project_path: 'src/MyApp.sln'
```

## Best Practices

- Use with a build workflow for full CI coverage.
- Upload test results for traceability.
- Use coverage tools for quality metrics.
