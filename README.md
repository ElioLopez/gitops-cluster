# gitops-cluster

Initial install on empty cluster (fresh installed)
kustomize build infrastructure/argocd/base | kubectl apply -f -