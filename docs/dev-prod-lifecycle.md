# Dev / Prod Lifecycle

## 1. Environment Separation

This repository enforces a clear separation between development and production environments through Argo CD sync policy.

## 2. Dev Environment

- Automatic reconciliation
- Continuous delivery behavior

## 3. Prod Environment

- Manual reconciliation
- Explicit promotion required

## 4. Promotion Model

Both environments share identical configuration structures and application artifacts.
