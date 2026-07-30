# yamllint-kubeconform

One composite action that **lints YAML** (`yamllint`) and **schema-validates Kubernetes
manifests** (`kubeconform`) — the two halves of "is this well-formed, and is it a valid
Kubernetes object?"

**Public and generic on purpose.** GitHub shares private actions only within an org, so
this stays public to be usable from any org (engagement orgs included). It contains no
SBE-specific logic.

## Usage

```yaml
- uses: sbe-devops/yamllint-kubeconform@v0.1.0
  with:
    paths: project/ appsets/
    exclude: '_template.yaml'      # scaffolds with placeholders: linted, not validated
```

### Inputs

| Input | Default | Notes |
|---|---|---|
| `paths` | *(required)* | Space-separated files/dirs |
| `lint` / `validate` | `true` | Toggle either half |
| `yamllint_config` | bundled | Block style enforced (inline `{}` forbidden) |
| `exclude` | `""` | Basename globs skipped during **validation** |
| `kubeconform_version` | `v0.8.0` | Pinned release |
| `schema_locations` | `default` + CRDs-catalog | CRs are **validated**, not skipped |
| `kubeconform_flags` | `-strict` | Appended to `-summary` |

## Why the bundled lint profile forbids inline `{}`

Expanded block YAML makes structural mistakes visible. The classic one:

```yaml
generators:
  - list:
    elements:        # ← sibling of `list`, not nested under it → empty generator
```

`kubeconform` catches it precisely (`/spec/generators/0/list: got null, want object`), and
the self-test asserts the action **fails** on exactly that fixture.

## Tooling note (community-conventions-first)

`yamllint` comes preinstalled on GitHub runners (no install step). `kubeconform` is
installed from its **pinned official release** rather than its Docker image — it is a single
static binary, so a container adds pull + startup cost per run for no runtime benefit, and a
Docker action only mounts `GITHUB_WORKSPACE`.
