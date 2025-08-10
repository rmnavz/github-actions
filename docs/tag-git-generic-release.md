# Tag Git (Generic Release) Workflow Documentation

This document describes the `tag-git-generic-release.yml` reusable workflow for creating and pushing a git tag using any provided string. This workflow is universal and not limited to semantic versioning.

## Purpose

- Create and push a git tag using any string (e.g., `1.2.3`, `release-2025-08-08`, `feature-xyz`).
- Supports annotated tags and tagging on multiple branches.
- Designed for universal use and workflow reusability.

## Usage Example

```yaml
jobs:
  tag-release:
    uses: rmnavz/github-actions/.github/workflows/tag-git-generic-release.yml@v1.0.0
    with:
      version: ${{ needs.get-version.outputs.version }}
      tag_prefix: 'v'
      tag_annotation: 'Release version'
      tag_branches: 'main,develop,release/'
```

## Inputs

| Name           | Type   | Required | Default                        | Description                                      |
|----------------|--------|----------|--------------------------------|--------------------------------------------------|
| version        | string | Yes      |                                | The string to use for the tag                    |
| tag_prefix     | string | No       | v                              | Prefix for the tag name                          |
| tag_annotation | string | No       |                                | Annotated tag message (optional)                 |
| tag_branches   | string | No       | main,develop,release/          | Comma-separated list of branches/tags to tag on   |

## Outputs

None

## Steps Overview

1. **Checkout Source Code**: Fetches the repository with full history.
2. **Check if Tag Exists**: Prevents duplicate tags.
3. **Create Git Tag**: Creates and pushes the tag if it does not exist.

## Best Practices

- Use this workflow as a reusable building block for tagging in CI/CD.
- Pin the workflow version and all action versions for reproducibility.
- Use meaningful tag names and annotations for traceability.

## Related Links

- [GitHub Actions Reusable Workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows)
- [Git Tag Documentation](https://git-scm.com/book/en/v2/Git-Basics-Tagging)

---
