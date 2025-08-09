# Publish Docs (Generic Pages) Workflow

This workflow publishes static documentation (e.g., DocFX) to GitHub Pages using a reusable workflow.


## Features

- Reusable via `workflow_call` in external repositories
- Supports any project with a valid DocFX configuration
- Minimal required permissions for GitHub Pages
- Customizable .NET SDK version
- Configurable DocFX version for security and reproducibility

## Inputs

| Name               | Type   | Required | Default | Description                                             |
|--------------------|--------|----------|---------|---------------------------------------------------------|
| docfx_project_path | string | Yes      | —       | Path to the DocFX project directory (relative to root)  |
| dotnet_version     | string | No       | 8.x     | .NET SDK version to use                                 |
| docfx_version      | string | No       | 2.78.3  | DocFX tool version to use. Allows pinning for security and reproducibility. |

## Outputs

| Name     | Description                        |
|----------|------------------------------------|
| page_url | URL of the deployed GitHub Pages   |

## Example Usage

```yaml
jobs:
  publish-docs:
    uses: your-org/github-actions/.github/workflows/publish-docs-generic-pages.yml@v1.0.0
    with:
      docfx_project_path: 'docs'
  dotnet_version: '8.x'
  docfx_version: '2.78.3'
```

## Notes

- The workflow requires a valid `docfx.json` in the specified directory.
- The workflow works for both .NET and non-.NET projects as long as DocFX is configured.
- The output site is expected at `<docfx_project_path>/_site` after build.
