# Argo CD Configuration

## 1. Configuration Scope

Argo CD manages both ApplicationSets and generated Applications using GitOps principles.

## 2. Meta-Application

A dedicated Argo CD Application manages all ApplicationSet resources and enforces:

- Automated synchronization
- Prune behavior
- Self-healing

## 3. Generated Applications

Each generated Application:

- Targets an isolated namespace
- Deploys the same Helm chart
- Applies environment-specific sync policies

## 4. Sync Policy Model

Dev reconciles automatically. Production reconciliation requires explicit promotion.
