## create sealed secrets

for synology CSI driver the sealed secrets are created from a yaml file:

```
cat client-info.yaml
clients:
- host: SYNOLOGY_IP
  username: USERNAME
  password: PASSWORD
  https: false
  port: 5000
```

```
kubectl create secret generic synology-csi \
--from-file=./client-info.yaml \
--output json --dry-run=client | kubeseal \
--scope cluster-wide \
-n kube-system  >  sealed-secrets.yaml
```

more info on: https://github.com/bitnami-labs/sealed-secrets