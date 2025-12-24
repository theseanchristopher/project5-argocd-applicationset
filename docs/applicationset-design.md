# ApplicationSet Design

## 1. Design Objective

The ApplicationSet defines a single declarative source for generating multiple environment-specific Argo CD Applications.

## 2. Generator Model

A list generator defines environment entries, including name and target namespace, enabling controlled and predictable Application generation.

## 3. Template Model

The Application template specifies:

- Helm chart repository and revision
- Chart path
- Helm parameters for image and replica configuration

This enforces separation between application packaging and deployment configuration.

## 4. Generated Applications

The ApplicationSet controller produces:

- A dev Application with automated reconciliation
- A prod Application with manual reconciliation
