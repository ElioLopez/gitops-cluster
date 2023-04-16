# gitops-cluster

Initial install on empty cluster (freshly installed)

```
kubectl apply -k .
```

## infrastructure diagram
![alt text](https://github.com/ElioLopez/gitops-cluster/blob/master/images/infrastructure-diagram.png?raw=true)

## infrastructure description

### Hypervisor
I've repurposed an old latitude laptop with proxmox to use it as an hypervisor.

### Kubernetes cluster
K3s was used to create a 4 node cluster on ubuntu 22.04.
It was installed with traefik enabled (default)

### Internal Network
I've set a wireless bridge between the speedport modem from the telekom and a TP-Link router in client mode.
So the small rack with the latitude laptop and the synology storage are connected to a netgear switch.
The whole internal network is transparently connected in the same 192.168.2.0/24 segment, so I can access internet, administer the cluster and argocd, traefik, etc only internally.
There are a few services that are reachable from the internet.
I've forwarded the traffic on the 443 port in the speedport modem to a node in the cluster (in the speedport the forward in only possible to predefined IPs, anyone will work, this traffic will be handled by traefik and routed properly)

```
eliolopez@MacBook-Pro-von-Elio  ~/repos/gitops-cluster/infrastructure   master ±  kubectl get nodes -o wide                                   
NAME           STATUS   ROLES                  AGE    VERSION        INTERNAL-IP     EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION      CONTAINER-RUNTIME
k3s-worker05   Ready    <none>                 78d    v1.25.6+k3s1   192.168.2.128   <none>        Ubuntu 22.04.1 LTS   5.15.0-60-generic   containerd://1.6.8-k3s1
k3s-master02   Ready    <none>                 130d   v1.25.3+k3s1   192.168.2.126   <none>        Ubuntu 22.04.1 LTS   5.15.0-60-generic   containerd://1.6.8-k3s1
k3s-master01   Ready    control-plane,master   146d   v1.25.3+k3s1   192.168.2.125   <none>        Ubuntu 22.04.1 LTS   5.15.0-60-generic   containerd://1.6.8-k3s1
k3s-worker04   Ready    <none>                 146d   v1.25.3+k3s1   192.168.2.151   <none>        Ubuntu 22.04.1 LTS   5.15.0-60-generic   containerd://1.6.8-k3s1
```

The traefik installed by k3s will create a daemonset creating an external IP on every node:
```
eliolopez@MacBook-Pro-von-Elio  ~/repos/gitops-cluster/infrastructure   master ±  kubectl get services traefik -n kube-system         
NAME      TYPE           CLUSTER-IP      EXTERNAL-IP                                               PORT(S)                                     AGE
traefik   LoadBalancer   10.43.158.120   192.168.2.125,192.168.2.126,192.168.2.128,192.168.2.151   9000:30982/TCP,80:32668/TCP,443:31254/TCP   6d7h
```

### Public Network
I'm using cloudflare as dns provider for the elizondo.cloud domain.
There are just a few services that are intended to be accesed externally (i.e. photoview)
