## create sealed secrets


more info on: https://github.com/bitnami-labs/sealed-secrets
```
kubectl create secret generic cloudflare-ddns \
--from-literal=RECORD_ID=xxxxxx \
--from-literal=NAME=xxxxxx \
--from-literal=PROXIED=true \
--from-literal=ZONE_ID=xxxxxx \
--from-literal=API_TOKEN=xxxxxx \
--output json --dry-run=client  | kubeseal \
--scope cluster-wide \
-n kube-system  > cloudflare-ddns-sealed-secrets.yml
```

To get the requested variables, we will need the API KEY (overview/API Tokens/ Global API key)
to get the zone ID first:

LIST AN EXISTING ZONE RECORD FOR A DOMAIN
```
EMAIL="pepe@grillo.com"; \
KEY="111222333444"; \
DOMAIN="example.com"
curl -X GET "https://api.cloudflare.com/client/v4/zones?name=$DOMAIN" \
    -H "X-Auth-Email: $EMAIL" \
    -H "X-Auth-Key: $KEY" \
    -H "Content-Type: application/json" \
    | python3 -m json.tool; 
```
then with the zone ID we will get the record ID

EMAIL="steve@example.com"; \
KEY="567422798b1238c43b64b5d16a2b89777ac6c"; \
ZONE_ID="360f44465ba1802a26bb40b5306b1b05"; \
curl -X GET "https://api.cloudflare.com/client/v4/zones/$ZONE_ID/dns_records" \
    -H "X-Auth-Email: $EMAIL" \
    -H "X-Auth-Key: $KEY" \
    -H "Content-Type: application/json" \
    | python3 -m json.tool;
