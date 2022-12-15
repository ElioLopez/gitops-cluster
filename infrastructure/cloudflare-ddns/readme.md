## create sealed secrets


more info on: https://github.com/bitnami-labs/sealed-secrets
```
kubectl create secret generic cloudflare-ddns \
--from-literal=RECORD_ID=xxxxxx \
--from-literal=NAME=xxxxxx \
--from-literal=PROXIED=true \
--from-literal=ZONE_ID=xxxxxx \
--from-literal=API_TOKEN=xxxxxx \
--output json --dry-run=client  | kubeseal --controller-name sealed-secrets -n kube-system  > cloudflare-ddns-sealed-secrets.yml
```
