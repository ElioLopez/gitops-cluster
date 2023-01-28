## create sealed secrets


more info on: https://github.com/bitnami-labs/sealed-secrets

secrets for postgres DB
```
kubectl create secret generic gitlab-postgres \
--from-literal=superUser=xxxx \
--from-literal=superUserPassword=xxxxxxx \
--from-literal=replicationUserPassword=xxxxxxx \
--output json --dry-run=client  | kubeseal \
--scope cluster-wide \
-n kube-system  > gitlab-postgres-sealed-secrets.yaml
```

secrets for redis
```
kubectl create secret generic gitlab-redis \
--from-literal=redisPassword=xxxxxxx \
--output json --dry-run=client  | kubeseal \
--scope cluster-wide \
-n kube-system  > gitlab-redis-sealed-secrets.yaml
```

secret for gitlab
```
kubectl create secret generic nextcloud \
--from-literal=username=xxxxxxx \
--from-literal=password=xxxxxxx \
--output json --dry-run=client  | kubeseal \
--scope cluster-wide \
-n kube-system  > nextcloud-sealed-secrets.yaml
```