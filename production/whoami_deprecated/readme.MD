This one is actually deprecated, but is saved here as documentation on how to handle the https termination entirely on the kubernetes cluster.

```
kubectl create secret generic \
origin-ca-service-key \
--from-literal=key='v1.xxxxxxx' \
--output json --dry-run=client  | kubeseal --controller-name sealed-secrets  \
--scope cluster-wide -n kube-system  > origin-ca-service-key.yaml
```

