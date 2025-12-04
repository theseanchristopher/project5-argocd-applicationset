# Project 5 Architecture

<img src="images/project5-architecture.svg" width="750">

This document explains the architecture of Project 5, which implements an Argo CD **ApplicationSet**-based GitOps model for managing multiple environments (dev and prod).

Project 5 builds on the earlier projects by:

- Using **Project 1** as the CI system (build + push + GitOps update)
- Using **Project 4** as the **Helm chart source** for the application
- Introducing **Project 5** as the **GitOps configuration repo** for ApplicationSets
- Having **Argo CD** pull configuration and manage rollouts in EKS

## High-Level Flow

1. Developer commits code to the Project 1 repository (branch `project5-gitops`).
2. GitHub Actions builds the Docker image and pushes it to ECR using the commit SHA as the image tag.
3. CI updates the `image.tag` value inside the **Project 5 ApplicationSet** (dev only).
4. Argo CD meta-application (`project5-applicationsets-app`) syncs the updated ApplicationSet.
5. The ApplicationSet controller updates the `project5-dev` Application.
6. Argo CD auto-syncs dev and rolls out the new image.
7. Prod promotion is controlled via a manual sync of `project5-prod`.

## Components

Key components:

- **Project 1 CI:** Builds and tags the image, updates GitOps config.
- **Project 4 Helm Chart:** Provides the Kubernetes manifests as a Helm chart.
- **Project 5 GitOps Repo:** Stores Argo CD ApplicationSet and meta-application definitions.
- **Argo CD ApplicationSet Controller:** Generates `project5-dev` and `project5-prod` Applications.
- **Argo CD Applications:** Manage synchronization and health of dev/prod namespaces.

## Diagram (Text)

```
Developer → Project 1 Repo → GitHub Actions CI
      → ECR Image
      → Project 5 GitOps Repo (ApplicationSet image.tag update)
      → Argo CD (project5-applicationsets-app)
      → ApplicationSet Controller
      → Argo CD Applications (project5-dev / project5-prod)
      → EKS Namespaces (project5-dev / project5-prod)
```
