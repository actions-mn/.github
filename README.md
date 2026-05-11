# actions-mn/.github

Shared reusable workflows for the [actions-mn](https://github.com/actions-mn) organization.

## Reusable Workflows

### `metanorma-generate.yml`

Builds a Metanorma site and deploys to GitHub Pages.

```yaml
jobs:
  site:
    uses: actions-mn/.github/.github/workflows/metanorma-generate.yml@v1
    secrets: inherit
```

**Inputs:**
| Input | Default | Description |
|-------|---------|-------------|
| `submodules` | `false` | Whether to checkout submodules |
| `container-image` | `metanorma/metanorma:latest` | Docker image for Metanorma |
| `deploy-branch` | `main` | Branch to deploy from |

### `metanorma-release.yml`

Creates per-document GitHub Releases with content-hash change detection.

```yaml
jobs:
  release:
    uses: actions-mn/.github/.github/workflows/metanorma-release.yml@v1
    with:
      default-visibility: private
    secrets: inherit
```

**Inputs:**
| Input | Default | Description |
|-------|---------|-------------|
| `submodules` | `false` | Whether to checkout submodules |
| `default-visibility` | `public` | Default visibility for unlisted documents |
| `include-pattern` | `*` | Glob pattern to filter documents |
| `force` | `false` | Force release even if unchanged |

**Visibility behavior** (with `default-visibility: private`):
- Documents listed in `metanorma.release.yml` without explicit visibility → public
- Documents listed with `visibility: private` → not released
- Documents NOT listed → not released (safe default)
