# Dev/Prod Lifecycle

Project 5 models a realistic lifecycle for dev and prod environments using ApplicationSets and Argo CD.

## Dev Environment

- Auto-sync enabled
- 1 replica (resource efficient)
- Receives new images on every successful CI run
- Ideal for fast iteration and validation

## Prod Environment

- Manual sync (no automatic rollout)
- Same Helm chart and ApplicationSet structure as dev
- Updated by syncing `project5-prod` in the Argo CD UI
- Represents a stable environment with explicit promotion

## Promotion Model

The promotion model is:

1. CI updates dev automatically.
2. Dev is tested and validated.
3. When ready, prod is updated by manually syncing the `project5-prod` Application.

This pattern is common in production GitOps setups.
