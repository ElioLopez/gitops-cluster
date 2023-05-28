to inject the CA on the cluster to be used for cert-manager, go to the folder where the ca and ca-key is located:

kubectl --namespace cert-manager \
  create secret tls k3s-ca-key-pair \
  --cert=ca.pem \
  --key=ca-key.pem \
  --output json --dry-run=client  | kubeseal  \
--scope cluster-wide -n kube-system  > ca-local-cluster-issuer.yaml