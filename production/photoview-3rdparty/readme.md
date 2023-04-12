## create sealed secrets


more info on: https://github.com/bitnami-labs/sealed-secrets

secrets for postgres DB
```
kubectl create secret generic photoview-postgres \
--from-literal=superUser=xxxxxxx \
--from-literal=superUserPassword=xxxxxxx \
--from-literal=replicationUserPassword=xxxxxxx \
--output json --dry-run=client  | kubeseal \
--scope cluster-wide \
-n kube-system  > postgres-sealed-secrets.yaml
```
