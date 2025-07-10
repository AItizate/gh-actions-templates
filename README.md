# Reusable GitHub Actions Workflows

This repository serves as a centralized collection of reusable workflows for common CI/CD tasks within the AItizate organization. The goal is to standardize and simplify automation across projects.

## How to Use

To use a reusable workflow in your repository, you need to call it from one of your own workflow files (e.g., in `.github/workflows/main.yml`). You must grant the necessary permissions for the actions to run correctly.

A typical job definition will look like this:

```yaml
jobs:
  call-reusable-workflow:
    # You must grant permissions for the called workflow to access the repository and write an OIDC token.
    permissions:
      contents: read
      id-token: write # Required for authenticating to AWS
    uses: AItizate/gh-actions-templates/.github/workflows/workflow-file-name.yml@main
    with:
      # ... your inputs ...
    secrets:
      # ... your secrets ...
```

---

## Available Workflows

### 1. Reusable - Build & Push Docker Image (AWS ECR)

**File:** `workflows/build-push-template.yml`

This workflow builds a Docker image from a specified Dockerfile and pushes it to an Amazon ECR repository.

#### Inputs

| Name             | Type   | Required | Default              | Description                                                              |
| ---------------- | ------ | -------- | -------------------- | ------------------------------------------------------------------------ |
| `branch`         | string | `true`   |                      | The branch to check out the code from.                                   |
| `ecr_repository` | string | `true`   |                      | The ECR repository to push the image to (e.g., `my-app/my-service`).     |
| `image_tag`      | string | `true`   | `testing`            | The tag for the Docker image (e.g., `latest`, `v1.0.0`).                 |
| `docker_file`    | string | `true`   | `./docker/Dockerfile` | The path to the Dockerfile.                                              |
| `aws_region`     | string | `true`   |                      | The AWS region where the ECR repository is located.                      |

#### Secrets

| Name                    | Required | Description                                                          |
| ----------------------- | -------- | -------------------------------------------------------------------- |
| `aws_access_key_id`     | `true`   | AWS Access Key ID for authenticating to ECR.                         |
| `aws_secret_access_key` | `true`   | AWS Secret Access Key for authenticating to ECR.                     |
| `github_package_token`  | `true`   | A GitHub token with `packages:read` permission for private packages. |

#### Outputs

| Name              | Description                                   |
| ----------------- | --------------------------------------------- |
| `docker_registry` | The full Docker registry and repository path. |
| `docker_image_tag`| The Docker image tag used for the build.      |

#### Example Usage

```yaml
# .github/workflows/ci.yml
name: Build and Push Main Branch

on:
  push:
    branches:
      - main

jobs:
  build-and-push:
    permissions:
      contents: read
      id-token: write
    uses: AItizate/gh-actions-templates/.github/workflows/build-push-template.yml@main
    with:
      branch: 'main'
      ecr_repository: 'my-app/my-production-service'
      image_tag: ${{ github.sha }}
      docker_file: './Dockerfile'
      aws_region: 'us-east-1'
    secrets:
      aws_access_key_id: ${{ secrets.AWS_ACCESS_KEY_ID }}
      aws_secret_access_key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      github_package_token: ${{ secrets.GITHUB_TOKEN }}
```

---

### 2. Reusable - Build & Push Docker Image (Generic)

**File:** `workflows/build-push-generic-template.yml`

This workflow builds a Docker image and pushes it to a generic, non-AWS private Docker registry.

#### Inputs

| Name              | Type   | Required | Default              | Description                                                              |
| ----------------- | ------ | -------- | -------------------- | ------------------------------------------------------------------------ |
| `branch`          | string | `true`   |                      | The branch to check out the code from.                                   |
| `registry_url`    | string | `true`   |                      | The URL of the private Docker registry.                                  |
| `repository_name` | string | `true`   |                      | The name of the repository to push to (e.g., `my-app/my-service`).     |
| `image_tag`       | string | `true`   | `testing`            | The tag for the Docker image (e.g., `latest`, `v1.0.0`).                 |
| `docker_file`     | string | `true`   | `./docker/Dockerfile` | The path to the Dockerfile.                                              |

#### Secrets

| Name                    | Required | Description                                                          |
| ----------------------- | -------- | -------------------------------------------------------------------- |
| `registry_username`     | `true`   | Username for the private Docker registry.                            |
| `registry_password`     | `true`   | Password or Access Token for the private Docker registry.            |
| `github_package_token`  | `true`   | A GitHub token with `packages:read` permission for private packages. |

#### Outputs

| Name               | Description                     |
| ------------------ | ------------------------------- |
| `docker_image_uri` | The full Docker image URI.      |

#### Example Usage

```yaml
# .github/workflows/ci-generic.yml
name: Build and Push to Generic Registry

on:
  push:
    branches:
      - main

jobs:
  build-and-push-generic:
    permissions:
      contents: read
    uses: AItizate/gh-actions-templates/.github/workflows/build-push-generic-template.yml@main
    with:
      branch: 'main'
      registry_url: 'my-private-registry.my-domain.com'
      repository_name: 'my-app/my-service'
      image_tag: ${{ github.sha }}
      docker_file: './Dockerfile'
    secrets:
      registry_username: ${{ secrets.REGISTRY_USERNAME }}
      registry_password: ${{ secrets.REGISTRY_PASSWORD }}
      github_package_token: ${{ secrets.GITHUB_TOKEN }}
```

---

### 3. Reusable - Deploy to EKS

**File:** `workflows/deploy-template.yml`

This workflow deploys a specified Docker image to a Kubernetes deployment on an Amazon EKS cluster.

#### Inputs

| Name                 | Type   | Required | Default     | Description                                                                                          |
| -------------------- | ------ | -------- | ----------- | ---------------------------------------------------------------------------------------------------- |
| `docker_image`       | string | `true`   |             | The full URI of the Docker image to deploy (e.g., `123456789012.dkr.ecr.us-east-1.amazonaws.com/my-app:latest`). |
| `k8s_cluster_name`   | string | `true`   |             | The name of the EKS cluster to deploy to.                                                            |
| `k8s_service`        | string | `false`  | `data-sync` | The name of the Kubernetes deployment/service to update.                                             |
| `k8s_namespace`      | string | `false`  | `default`   | The Kubernetes namespace where the service is located.                                               |
| `k8s_container_name` | string | `false`  | `data-sync` | The name of the container within the deployment to update.                                           |
| `aws_region`         | string | `true`   |             | The AWS region where the EKS cluster is located.                                                     |

#### Secrets

| Name                    | Required | Description                             |
| ----------------------- | -------- | --------------------------------------- |
| `aws_access_key_id`     | `true`   | AWS Access Key ID for EKS access.       |
| `aws_secret_access_key` | `true`   | AWS Secret Access Key for EKS access.   |

#### Example Usage

```yaml
# .github/workflows/cd.yml
name: Deploy to Production

on:
  workflow_run:
    workflows: ["Build and Push Main Branch"]
    types:
      - completed

jobs:
  deploy-to-prod:
    permissions:
      contents: read
      id-token: write
    uses: AItizate/gh-actions-templates/.github/workflows/deploy-template.yml@main
    with:
      # This assumes the build workflow returns the image URI as an output
      docker_image: ${{ needs.build-job.outputs.docker_registry }}:${{ needs.build-job.outputs.docker_image_tag }}
      k8s_cluster_name: 'my-prod-cluster'
      k8s_service: 'my-production-service'
      k8s_namespace: 'production'
      k8s_container_name: 'app'
      aws_region: 'us-east-1'
    secrets:
      aws_access_key_id: ${{ secrets.AWS_ACCESS_KEY_ID }}
      aws_secret_access_key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```
