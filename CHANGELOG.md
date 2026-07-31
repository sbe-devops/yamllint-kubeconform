# Changelog

Format loosely follows [Keep a Changelog](https://keepachangelog.com/); versioning is
[SemVer](https://semver.org/).

## [0.2.0]

### Changed

- **kubeconform is installed by `sbe-devops/gh-setup-kubeconform@v0.1.0`** instead of an inline
  `curl`. Verified against published checksums, fails closed, and resolves the platform rather
  than hardcoding it. The same install previously existed here *and* in `helm-kustomize` — now
  one install, one place to audit.
- **`kubeconform_version` no longer takes a leading `v`** (`v0.8.0` → `0.8.0`).

## [0.1.0]

### Added

- Initial release: `yamllint` + `kubeconform` in one composite action, with a bundled
  block-style lint profile, CRDs-catalog schema locations (CRs validated, not skipped),
  and a validation-only `exclude` for placeholder scaffolds.
- Self-test asserts the action **passes** a good manifest and **fails** a mis-nested
  ApplicationSet.
