# AItizate gh-actions-templates

> Reusable GitHub Actions workflows for the AItizate ecosystem and anyone else who wants them.

A small, opinionated library of workflow templates that solve the recurring CI/CD problems we hit across our repos: build + scan + push container images, validate PRs, tag releases, notify on failures. Each template is a single file you can call from your own `.github/workflows/`.

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)
[![Latest release](https://img.shields.io/github/v/release/AItizate/gh-actions-templates)](https://github.com/AItizate/gh-actions-templates/releases)

## Why this exists

If every team writes their own `build → push → deploy` workflow, every team accumulates the same drift: missed security scans, inconsistent tags, half-rotated secrets, divergent failure handling. These templates are the version we keep current so individual repos don't have to.

## How to use

Pin to a **major tag** (recommended) so chart updates here don't surprise your CI:

```yaml
jobs:
  build:
    permissions:
      contents: read
      id-token: write
    uses: AItizate/gh-actions-templates/.github/workflows/build-push-generic-template.yml@v1
    with:
      branch: main
      registry_url: ghcr.io
      repository_name: my-org/my-app
      image_tag: ${{ github.sha }}
      docker_file: ./Dockerfile
    secrets:
      registry_username: ${{ secrets.GHCR_USER }}
      registry_password: ${{ secrets.GHCR_TOKEN }}
      github_package_token: ${{ secrets.GITHUB_TOKEN }}
```

| Pin you can use | Behaviour |
|-----------------|-----------|
| `@v1` (recommended) | Rolls forward inside the v1 line. New features, no breaking changes. |
| `@v1.2.3` | Exact version. Never moves. |
| `@main` | Rolling latest. **May break without warning.** Use only for testing the next release. |

## Template catalog

| Template | Use it for | Source |
|----------|------------|--------|
| `build-push-generic-template.yml` | Build + **Trivy scan** + push to any generic Docker registry (since v1.1) | [.yml](.github/workflows/build-push-generic-template.yml) |
| `build-push-template.yml` | Build + push to AWS ECR | [.yml](.github/workflows/build-push-template.yml) |
| `build-push-ecr-template.yml` | Build + push to AWS ECR (alternate IAM flow) | [.yml](.github/workflows/build-push-ecr-template.yml) |
| `pr-validation-template.yml` | Conventional Commits validation on PRs (sticky comment + optional blocking) (since v1.1) | [.yml](.github/workflows/pr-validation-template.yml) |
| `release-tag-template.yml` | Create a Git tag + GitHub Release with auto-generated notes (since v1.1) | [.yml](.github/workflows/release-tag-template.yml) |
| `webhook-notification-template.yml` | Post a Slack-compatible JSON payload to any webhook URL (since v1.1) | [.yml](.github/workflows/webhook-notification-template.yml) |
| `deploy-template.yml` | `kubectl set image` on EKS (legacy — prefer GitOps) | [.yml](.github/workflows/deploy-template.yml) |

See the [CHANGELOG](CHANGELOG.md) for what's in each release and what's in progress.

## Conventions

- **Each template is a single workflow file** that exposes its inputs/secrets contract via `workflow_call`.
- **No hardcoded environment values.** Everything is an input or a secret.
- **One responsibility per template.** Compose templates from the calling repo, don't fork them.
- **Breaking changes get a major version bump.** Consumers pinned to `@v1` won't see them; consumers on `@main` should expect to fix things occasionally.

## Examples in the wild

- [`AItizate/forjate`](https://github.com/AItizate/forjate) — uses these templates from its consumer repos and ships `sync-app-image.yml` to close the GitOps loop.

## Contributing

1. Fork or branch off `main`.
2. Make your change. If it's a new template, copy an existing one as a starting point and respect the `workflow_call` shape.
3. Update [`CHANGELOG.md`](CHANGELOG.md) under `## [Unreleased]`.
4. Open a PR. CODEOWNERS will pick it up.

Breaking changes welcome — they just have to be honest about it (new major version, CHANGELOG entry, migration note).

## License

[Apache 2.0](LICENSE) — use these workflows in any project, public or private. Attribution appreciated but not required.
