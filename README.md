# VEuPathDB/.github

Organization-wide GitHub configuration for VEuPathDB.

- `profile/README.md` — the public profile shown at https://github.com/VEuPathDB
- `.github/workflows/` — reusable GitHub Actions workflows shared across VEuPathDB repositories

## Reusable workflows

### `nextflow-lint.yml`

Runs [`nextflow lint`](https://docs.seqera.io/nextflow/reference/cli) against a repository.
The job fails on lint errors (code Nextflow will refuse to run); warnings are reported in the job summary
without failing the build.

Add `.github/workflows/nextflow-lint.yml` to a Nextflow repository:

```yaml
name: Nextflow lint

on:
  push:
  pull_request:

jobs:
  lint:
    uses: VEuPathDB/.github/.github/workflows/nextflow-lint.yml@main
```

Optional inputs:

| Input              | Default   | Description                                          |
|--------------------|-----------|------------------------------------------------------|
| `nextflow-version` | `26.10.0` | Nextflow version used for linting                    |
| `paths`            | `.`       | Space-separated paths to lint, relative to repo root |

```yaml
jobs:
  lint:
    uses: VEuPathDB/.github/.github/workflows/nextflow-lint.yml@main
    with:
      paths: main.nf modules
```

To check locally before pushing:

```bash
nextflow lint .
```
