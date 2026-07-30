# Changelog

Format loosely follows [Keep a Changelog](https://keepachangelog.com/); versioning is
[SemVer](https://semver.org/).

## [0.1.0]

### Added

- Initial release: `yamllint` + `kubeconform` in one composite action, with a bundled
  block-style lint profile, CRDs-catalog schema locations (CRs validated, not skipped),
  and a validation-only `exclude` for placeholder scaffolds.
- Self-test asserts the action **passes** a good manifest and **fails** a mis-nested
  ApplicationSet.
