## create sealed secrets

more info on: https://github.com/bitnami-labs/sealed-secrets
```
kubectl create secret generic argocd-tls \
--from-literal=tls.crt=############ \
--from-literal=tls.key=############ \
--output json --dry-run=client  | kubeseal \ 
--scope cluster-wide \ 
--controller-name sealed-secrets \ 
-n kube-system  > argocd-tls.yml
```
