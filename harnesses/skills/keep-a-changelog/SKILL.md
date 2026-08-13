---
name: keep-a-changelog
description: Create and maintain CHANGELOG.md using Keep a Changelog 1.1.0 and SemVer. Use when adding release notes, updating Unreleased, or initializing a changelog. Ask which language to use before writing.
---

# Keep a Changelog 1.1.0

Source of truth: https://keepachangelog.com/en/1.1.0/

Companion versioning: https://semver.org/spec/v2.0.0.html

## First step — choose language

Before creating or editing `CHANGELOG.md`, ask which language to write entries in
(for example English or Russian). Remember the answer for the rest of the session
and keep the whole file in that language, including section headings if the user
wants localized headings. Default section headings stay English
(`Added` / `Changed` / …) unless the user asks otherwise.

Do not write changelog content until the language is confirmed.

## File

Prefer `CHANGELOG.md` at the repository root.

Starter skeleton:

```markdown
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added

- First notable change.
```

## Guiding principles

- Changelogs are for humans, not machines.
- There should be an entry for every released version.
- Group the same types of changes together.
- Versions and sections should be linkable.
- Latest version comes first.
- Show each version's release date as `YYYY-MM-DD` (ISO 8601).
- Say whether the project follows Semantic Versioning.

## Types of changes

- `Added` — new features
- `Changed` — changes in existing functionality
- `Deprecated` — soon-to-be removed features
- `Removed` — now removed features
- `Fixed` — bug fixes
- `Security` — vulnerability fixes

Omit empty sections.

## Workflow

1. Ask for changelog language if not already known.
2. Open or create `CHANGELOG.md`.
3. Put in-progress notes under `## [Unreleased]`.
4. On release, move Unreleased items into `## [X.Y.Z] - YYYY-MM-DD`.
5. Keep only notable user/contributor-facing changes — not raw git noise.
6. Call out deprecations, removals, and breaking changes explicitly.
7. For yanked releases, keep the version and mark it: `## [0.0.5] - 2014-12-13 [YANKED]`
8. Add comparison links at the bottom when the project uses git tags.

## Anti-patterns

- Dumping commit log diffs as the changelog
- Hiding deprecations or breaking changes
- Ambiguous regional dates instead of `YYYY-MM-DD`
- Inconsistent coverage that makes the file look complete when it is not

## Example release section

```markdown
## [Unreleased]

## [1.1.0] - 2026-08-13

### Added

- Agent bootstrap skill for selecting harnesses.

### Fixed

- Catalog install paths for project-local skills.

[unreleased]: https://github.com/org/repo/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/org/repo/releases/tag/v1.1.0
```
