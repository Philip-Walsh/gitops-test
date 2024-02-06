# Gitops with Flux

This repository contains the configuration files for managing Kubernetes clusters using GitOps principles. The project is structured as follows:

## Clusters

### my-cluster

- **flux-system**: Contains configuration for Flux, the GitOps operator.

  - **gotk-components.yaml**: Defines the components of Flux.
  - **gotk-sync.yaml**: Specifies the synchronization settings for Flux.
  - **kustomization.yaml**: Kustomization file for Flux system components.

- **simple-web-server-with-nodeport.yaml**: YAML manifest for deploying a simple web server with a NodePort service.

- **weave-gitops-dashboard.yaml**: YAML manifest for deploying the Weave GitOps Dashboard.
