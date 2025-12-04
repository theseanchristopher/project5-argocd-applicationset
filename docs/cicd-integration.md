# CI/CD Integration

This document explains how Project 5 integrates with the CI pipeline defined in Project 1.

## Workflow

1. Docker image is built and pushed to ECR.
2. The commit SHA is used as the image tag.
3. The Project 5 GitOps repo (`project5-argocd-applicationset`) is checked out.
4. The `image.tag` parameter in the **dev ApplicationSet** is updated.
5. The change is committed and pushed to the `main` branch of Project 5.
6. Argo CD meta-application (`project5-applicationsets-app`) auto-syncs the ApplicationSet.
7. The `project5-dev` Application becomes OutOfSync and auto-syncs, rolling out the new image.

## Prod Promotion

Prod deployment requires:

1. Confirming dev looks healthy.
2. Manually syncing the `project5-prod` Application in the Argo CD UI.

This separates continuous delivery (dev) from controlled promotion (prod).
