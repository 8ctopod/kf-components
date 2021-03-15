# Setup Kubeflow to Run Locally
## Create local cluster (on macos)
```bash
$ brew install kind
$ kind create cluster
```
## Deploy kubeflow pipelines
```bash
# env/platform-agnostic-pns hasn't been publically released, so you will install it from master
$ export PIPELINE_VERSION=1.4.1
$ kubectl apply -k "github.com/kubeflow/pipelines/manifests/kustomize/cluster-scoped-resources?ref=$PIPELINE_VERSION"
$ kubectl wait --for condition=established --timeout=60s crd/applications.app.k8s.io
$ kubectl apply -k "github.com/kubeflow/pipelines/manifests/kustomize/env/platform-agnostic-pns?ref=$PIPELINE_VERSION"
```
## Verify that the Kubeflow Pipelines UI is accessible by port-forwarding:
```bash
$ kubectl port-forward -n kubeflow svc/ml-pipeline-ui 8080:80
```
## Connect to the Kubeflow UI
Accessible at `http://127.0.0.1:8080/#/pipelines`