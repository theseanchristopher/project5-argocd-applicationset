# Project 5 – Argo CD ApplicationSet

This repository defines Argo CD ApplicationSet configuration to manage multiple environments (dev and prod) for the sample Nginx application from earlier projects.

## Goals

- Use Argo CD ApplicationSet to generate Argo CD Applications per environment.
- Dev environment: automated sync.
- Prod environment: manual sync (promotion).
- Integrate with the existing CI pipeline to update image tags for dev, with manual promotion to prod.

