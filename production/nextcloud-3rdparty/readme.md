## create sealed secrets


more info on: https://github.com/bitnami-labs/sealed-secrets

secrets for postgres DB
```
kubectl create secret generic nextcloud-postgres \
--from-literal=superUser=xxxxxxx \
--from-literal=superUserPassword=xxxxxxx \
--from-literal=replicationUserPassword=xxxxxxx \
--output json --dry-run=client  | kubeseal \
--scope cluster-wide \
--controller-name sealed-secrets \
-n kube-system  > nextcloud-postgres-sealed-secrets.yaml
```
secret for nextcloud
```
kubectl create secret generic nextcloud \
--from-literal=username=xxxxxxx \
--from-literal=password=xxxxxxx \
--output json --dry-run=client  | kubeseal \
--scope cluster-wide \
--controller-name sealed-secrets \
-n kube-system  > nextcloud-sealed-secrets.yaml
```