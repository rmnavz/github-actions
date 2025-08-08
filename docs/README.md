# GitHub Actions Workflows Overview

This repository provides a set of reusable GitHub Actions workflows for .NET and general CI/CD automation. Below is a summary of each workflow and its intended use.

---

## Workflows

### 1. version-semver-generic-ci.yml

- **Purpose:** Determines a semantic version using GitVersion (language-agnostic) and outputs it for use by other workflows (no tagging).
- **Inputs:** `gitversion_version`, `gitversion_config`
- **Outputs:** `semver`, `major`, `minor`, `patch`, `fullSemVer`
- **Docs:** No dedicated doc file; see workflow header for details.

### 2. build-solution-dotnet-ci.yml

- **Purpose:** Builds a .NET solution or project, caches dependencies, and optionally uploads build artifacts. Designed for universal use via `workflow_call`.
- **Inputs:** `dotnet_version`, `project_path`, `artifact_name`, `artifact_paths`, `artifact_retention_days`, `upload_artifacts`
- **Outputs:** `build_status`, `artifact_url`
- **Docs:** [docs/build-solution-dotnet-ci.md](build-solution-dotnet-ci.md)

### 3. test-solution-dotnet-unit-tests.yml

- **Purpose:** Runs tests for a .NET solution or project, collects coverage, and uploads test results as artifacts. Designed for universal use via `workflow_call`.
- **Inputs:** `dotnet_version`, `project_path`, `use_build_artifact`, `build_artifact_name`, `test_results_artifact_name`, `test_results_paths`, `test_results_retention_days`
- **Docs:** [docs/test-solution-dotnet-unit-tests.md](test-solution-dotnet-unit-tests.md)

### 4. build-package-dotnet-ci.yml

- **Purpose:** Builds and packages a .NET project for any versioning scheme. Uploads NuGet packages as artifacts. Designed for universal use and workflow reusability.
- **Inputs:** `release_version`, `dotnet_version`, `project_path`, `artifact_name`, `artifact_paths`, `artifact_retention_days`, `upload_artifacts`
- **Outputs:** NuGet package artifact(s)
- **Docs:** [docs/build-package-dotnet-ci.md](build-package-dotnet-ci.md)

### 5. publish-package-dotnet-release.yml

- **Purpose:** Publishes NuGet packages using any versioning scheme and creates a GitHub release. Designed for universal use and workflow reusability.
- **Inputs:** `release_version`, `prerelease`, `include_test_results`, `artifact_name`
- **Secrets:** `NUGET_API_KEY`, `GITHUB_TOKEN`
- **Outputs:** `release_url`
- **Docs:** [docs/publish-package-dotnet-release.md](publish-package-dotnet-release.md)

### 6. tag-git-generic-release.yml

- **Purpose:** Creates and pushes a git tag using any provided string (universal, not limited to semantic versioning).
- **Inputs:** `version`, `tag_prefix`, `tag_annotation`, `tag_branches`
- **Docs:** No dedicated doc file; see workflow header for details.

---

## Usage

- Each workflow is designed for reusability via `workflow_call` and can be referenced from other workflows in your repository or organization.
- For input/output details and usage examples, see the header comments in each workflow file or the linked documentation files.

---

## See Also

- [GitHub Actions Documentation](https://docs.github.com/en/actions)
- [Reusable Workflows](https://docs.github.com/en/actions/using-workflows/reusing-workflows)
