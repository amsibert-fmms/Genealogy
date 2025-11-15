# GeneaX Changelog Template {#geneax-changelog}
_Last updated: 2025-11-15_

Related references: [Developer hub](README.md#geneax-developer-hub) · [Documentation home](../index.md#geneax-docs-home)

Document releases and notable changes here. Follow [Keep a Changelog](https://keepachangelog.com/) conventions and align version
tags with Git releases.

## How to update
1. Add a new section under **Unreleased** for in-progress work.
2. When publishing, create a heading with the version number and date (`YYYY-MM-DD`).
3. Categorise entries under **Added**, **Changed**, **Fixed**, **Removed**, or **Security**.
4. Link back to relevant pull requests or issues.

## Template
```markdown
## [Unreleased]
### Added
-

### Changed
-

### Fixed
-

### Removed
-

### Security
-
```

## Example
```markdown
## [0.1.0] — 2025-11-15
### Added
- Initial GEDCOM X model definitions.
- ProofStatement schema and API endpoints.
- Draft validation logic for persons and relationships.

### Changed
- Updated CrossReference enum handling to support new numbering schemes.

### Security
- Documented vulnerability reporting workflow.
```

When you cut a release, tag the commit (`git tag v0.1.0 && git push --tags`) and update this file alongside the
[deployment playbook](deployment.md).
