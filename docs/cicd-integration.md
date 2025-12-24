# CI / GitOps Integration

## 1. Responsibility Boundary

This repository does not define CI pipelines.

## 2. Integration Contract

Image tags are updated upstream by an external CI system. Once committed, Argo CD reconciles the generated Applications based on the desired state defined in Git.

This establishes a strict separation between CI responsibilities and GitOps configuration management.
