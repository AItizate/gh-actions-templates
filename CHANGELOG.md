# Changelog

All notable changes to this repo are documented here. The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this project
adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

Consumers should **pin to a major tag** (e.g. `@v1`) rather than `@main`.
Breaking changes only happen on major version bumps.

## [Unreleased]

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

[Unreleased]: https://github.com/AItizate/gh-actions-templates/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/AItizate/gh-actions-templates/releases/tag/v1.0.0
