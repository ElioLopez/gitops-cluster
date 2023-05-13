```
kubectl create secret generic \
origin-ca-service-key \
--from-literal=key='v1.xxxxxxx' \
--output json --dry-run=client  | kubeseal --controller-name sealed-secrets  \
--scope cluster-wide -n kube-system  > origin-ca-service-key.yaml
```

