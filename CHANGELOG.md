# Changelog

All notable changes to this repo are documented here. The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project
adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Consumers should **pin to a major tag** (e.g. `@v1`) rather than `@main`.
Breaking changes only happen on major version bumps.

## [Unreleased]

## [1.1.0] — 2026-05-24

Security + automation pass. Four template changes, all backward-compatible
for consumers pinned to `@v1`.

### Added

- `pr-validation-template.yml` — validates PR title and commit messages
  against the Conventional Commits spec. Posts a sticky comment on the
  PR with the verdict. Optional `require_conventional_commits` input to
  fail the workflow.
- `release-tag-template.yml` — given a semver string, creates a Git tag
  and a GitHub Release with auto-generated notes. Validates the version
  format and refuses to overwrite an existing tag. Supports prereleases
  and explicit `target_commitish`.
- `webhook-notification-template.yml` — posts a JSON `{"text": "..."}`
  payload to any Slack-compatible webhook URL (Slack, Discord,
  Mattermost). Default failure message; overridable via `message` input.

### Changed

- `build-push-generic-template.yml` — now scans the built image with
  **Trivy before pushing**. Vulnerable images never reach the registry
  by default. New optional inputs (all backward-compatible defaults):
    - `push_image` (default: `true`) — set to `false` to build + scan only.
    - `trivy_severity` (default: `'CRITICAL,HIGH'`).
    - `trivy_exit_code` (default: `'1'`) — set to `'0'` for advisory-only scanning.
    - `trivy_ignore_unfixed` (default: `true`).

  Internal refactor: `docker/build-push-action` now uses `load: true`
  instead of `push: true`, with a separate `docker push` step gated on
  `inputs.push_image`. Existing consumers see no behaviour change.

### Bumped action versions

- `actions/checkout@v3` → `@v4`
- `docker/login-action@v2` → `@v3`

## [1.0.0] — 2026-05-24

First publicly available release. This is the baseline that the AItizate
internal repos have been consuming privately for some time. No behaviour
changes from the last private commit.

### Workflows

- `build-push-template.yml` — Build a Docker image and push it to AWS ECR.
- `build-push-ecr-template.yml` — Variant of the ECR build/push.
- `build-push-generic-template.yml` — Build + push to any generic Docker registry.
- `deploy-template.yml` — `kubectl set image` on an EKS deployment.

### Added (with the public release)

- `LICENSE` — Apache 2.0.
- `CHANGELOG.md` — this file.
- `CODEOWNERS` — review ownership.
- README rewrite documenting tag-pinning convention and contribution model.

[Unreleased]: https://github.com/AItizate/gh-actions-templates/compare/v1.1.0...HEAD
[1.1.0]: https://github.com/AItizate/gh-actions-templates/releases/tag/v1.1.0
[1.0.0]: https://github.com/AItizate/gh-actions-templates/releases/tag/v1.0.0
