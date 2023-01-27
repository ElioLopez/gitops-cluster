## create sealed secrets


more info on: https://github.com/bitnami-labs/sealed-secrets

secrets for postgres DB
```
kubectl create secret generic gitlab-postgres \
--from-literal=superUser=admin \
--from-literal=superUserPassword=6Dvr4882Lf8NN6 \
--from-literal=replicationUserPassword=N83UZ3VV22UbmT \
--output json --dry-run=client  | kubeseal \
--scope cluster-wide \
--controller-name sealed-secrets \
-n kube-system  > gitlab-postgres-sealed-secrets.yaml
```
secret for gitlab
```
kubectl create secret generic nextcloud \
--from-literal=username=xxxxxxx \
--from-literal=password=xxxxxxx \
--output json --dry-run=client  | kubeseal \
--scope cluster-wide \
--controller-name sealed-secrets \
-n kube-system  > nextcloud-sealed-secrets.yaml
```