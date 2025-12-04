# Argo CD Configuration

This document describes the Argo CD configuration used in Project 5.

## Meta-Application

Project 5 defines a **meta-application** in:

```
applications/project5-applicationsets-app.yaml
```

This Application:

- Points to this repo (`project5-argocd-applicationset`)
- Watches the `applicationsets/` directory
- Auto-syncs changes to the ApplicationSet definitions
- Enables prune + self-heal

By managing the ApplicationSet through Argo CD, the configuration itself is under GitOps control.

## Generated Applications

The ApplicationSet generates two Applications:

- `project5-dev` (auto-sync)
- `project5-prod` (manual sync)

Each Application:

- Uses the Project 4 Helm chart (`charts/app`)
- Deploys to its own namespace (`project5-dev` or `project5-prod`)
- Includes Argo CD sync status and health checking

## Sync Policies

Dev:

- Automated sync
- Immediate rollout on ApplicationSet changes

Prod:

- Manual sync
- Requires explicit promotion action in the Argo CD UI

These policies model a realistic separation between continuous delivery to dev and controlled promotion to production.
