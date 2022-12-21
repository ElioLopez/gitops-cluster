## create sealed secrets

for synology CSI driver the sealed secrets are created from a yaml file
more info on: https://github.com/bitnami-labs/sealed-secrets

```
kubectl create secret generic synology-csi \
--from-file=./client-info.yaml \
--output json --dry-run=client | kubeseal \
--scope cluster-wide \
--controller-name sealed-secrets \
-n kube-system  >  synology-csi-sealed-secrets.yml
```