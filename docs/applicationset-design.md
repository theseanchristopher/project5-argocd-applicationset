# ApplicationSet Design

This document describes how the ApplicationSet in Project 5 is designed to generate environment-specific Argo CD Applications for dev and prod.

## Generators

Project 5 uses a **list generator** to define environment entries such as:

- `name: dev`, `namespace: project5-dev`
- `name: prod`, `namespace: project5-prod`

This keeps environment configuration declarative and easy to extend.

## Template

The ApplicationSet `template` defines the common Application spec, including:

- `spec.source.repoURL` → Project 4 Helm Git repo  
- `spec.source.targetRevision` → `project4-gitops` branch  
- `spec.source.path` → `charts/app`  
- `spec.source.helm.parameters`:
  - `image.repository`
  - `image.tag`
  - `replicaCount`

These parameters allow CI to update only the tag while keeping chart logic in Project 4.

## Output Applications

The ApplicationSet controller produces:

- **project5-dev**
  - Auto-sync enabled
  - Uses latest `image.tag` from CI updates
  - Deploys to `project5-dev` namespace

- **project5-prod**
  - Manual sync (promotion only when operator approves)
  - Uses the same chart and parameter structure
  - Deploys to `project5-prod` namespace

This structure demonstrates a scalable, pattern-driven approach to managing multiple environments.
