# .NET Security Check

This workflow checks for vulnerable .NET packages and optionally runs CodeQL analysis. It is designed for universal use via `workflow_call` in other repositories.

## Purpose

The workflow helps identify security vulnerabilities in .NET projects by:

1. Scanning for vulnerable NuGet packages (including transitive dependencies)
2. Optionally running CodeQL analysis for deeper security insights

## Inputs

| Name | Description | Type | Required | Default |
|------|-------------|------|----------|---------|
| `dotnet_version` | .NET SDK version to use | string | No | `8.0.x` |
| `run_vulnerability_check` | Whether to run dotnet package vulnerability check | boolean | No | `true` |
| `run_codeql` | Whether to run CodeQL analysis | boolean | No | `false` |

## Outputs

| Name | Description |
|------|-------------|
| `vulnerability_status` | Status of vulnerability check. Will be `found` if vulnerabilities are detected, or `none` if no vulnerabilities are found. |

## Usage Examples

### Basic Usage

```yaml
jobs:
  security-check:
    uses: rmnavz/github-actions/.github/workflows/dotnet-security-check.yml@v1.0.0
    with:
      dotnet_version: '8.0.x'
```

### Complete Example with All Options

```yaml
jobs:
  security-check:
    uses: rmnavz/github-actions/.github/workflows/dotnet-security-check.yml@v1.0.0
    with:
      dotnet_version: '8.0.x'
      run_vulnerability_check: true
      run_codeql: true
```

### Using the Output in Subsequent Jobs

```yaml
jobs:
  security-check:
    uses: rmnavz/github-actions/.github/workflows/dotnet-security-check.yml@v1.0.0

  alert-if-vulnerabilities:
    needs: security-check
    if: needs.security-check.outputs.vulnerability_status == 'found'
    runs-on: ubuntu-latest
    steps:
      - name: Send Alert
        run: |
          echo "Vulnerabilities were found! Taking action..."
          # Add steps to notify team, create issues, etc.
```

## Workflow Details

1. The workflow checks out the source code
2. Sets up the specified .NET SDK version
3. Runs a vulnerability check on all packages (including transitive dependencies) if enabled
4. Runs CodeQL analysis if enabled
5. Creates a summary report of findings

## Best Practices

- Always run this workflow as part of your CI pipeline to catch security issues early
- Consider enabling CodeQL analysis for more comprehensive security checks
- Use the workflow's output to conditionally trigger actions based on security findings
