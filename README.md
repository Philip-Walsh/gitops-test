# GitOps with Flux

This repository is dedicated to managing Kubernetes clusters using GitOps principles. Below is the breakdown of its structure:

## Clusters

### my-cluster

- **flux-system**: Contains configuration for Flux, the GitOps operator.
  - **gotk-components.yaml**: Defines Flux components.
  - **gotk-sync.yaml**: Specifies synchronization settings.
  - **kustomization.yaml**: Kustomization file for Flux system components.
- **simple-web-server-with-nodeport.yaml**: YAML manifest for deploying a basic web server with a NodePort service.

- **weave-gitops-dashboard.yaml**: YAML manifest for deploying the Weave GitOps Dashboard.

## Requirements

- Kubernetes cluster set up with Minikube or another solution.
- kubectl configured to interact with the cluster.
- Flux installed. Installation instructions can be found [here](https://fluxcd.io/flux/installation/).

## Setup

1. Fork this repository with your preferred name.
2. Obtain a GitHub token as per the instructions [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).
3. Export the GitHub token and your GitHub username as environment variables:

   ```bash
   export GITHUB_TOKEN=<your token>
   export GITHUB_USER=<your user name>
   export GITHUB_REPO_NAME=<the name of this forked repo>
   ```

4. Bootstrap Flux on your GitHub repository:

   ```bash
   flux bootstrap github \
   --owner=$GITHUB_USER \
   --repository=$GITHUB_REPO_NAME \
   --branch=main \
   --path=./clusters/my-cluster \
   --personal
   ```

   - `owner` refers to your GitHub username.
   - `repository` is the name of your repository.
   - `branch` indicates the branch to track.
   - `path` specifies the directory for GitOps manifests.
   - Use `--personal` for personal accounts. For organizations, replace it with `--organization=<your organization>`.

## Exposing Services

You can expose services using the Weave GitOps Dashboard or directly through kubectl. For example:

To expose the Weave GitOps Dashboard:

```bash
kubectl port-forward svc/ww-gitops-weave-gitops -n flux-system 9001:9001
```

To expose nginx:

```bash
kubectl port-forward svc/my-nginx -n flux-system 8080:80
```

login with admin:password

For more information on Weave GitOps, refer to the [documentation](https://docs.gitops.weave.works/docs/intro-weave-gitops/).
