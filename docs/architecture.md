# Architecture

<img src="images/project5-architecture.svg" width="750">

## 1. Architecture Overview

This repository defines an Argo CD ApplicationSet-based GitOps architecture for managing multiple Kubernetes environments from a single declarative configuration source.

## 2. Core Components

- **GitOps Configuration Repository**: Stores ApplicationSet and meta-application definitions.
- **Helm Chart Repository**: Provides application manifests.
- **Argo CD**: Reconciles desired state and enforces synchronization policies.
- **ApplicationSet Controller**: Generates environment-specific Argo CD Applications.

## 3. Reconciliation Model

Argo CD continuously reconciles generated Applications against the desired state stored in Git. Environment behavior is governed by sync policy rather than by divergent configuration sources.

## 4. Control Flow

Developer → CI → GitOps configuration update → Argo CD meta-application → ApplicationSet controller → Argo CD Applications → Kubernetes namespaces

## 5. Environment Boundaries

Dev and prod environments are isolated by namespace and Argo CD sync policy while sharing a common application definition.
