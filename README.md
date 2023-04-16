# gitops-cluster

Initial install on empty cluster (fresh installed)

kubectl apply -k .

## infrastructure diagram
![alt text](https://github.com/ElioLopez/gitops-cluster/blob/main/images/infrastructure-diagram.png?raw=true)

## infrastructure description

I've repurposed an old latitude laptop with proxmox to use it as an hypervisor.
K3s was used to create a 4 node cluster
