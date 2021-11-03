---
title : DNS Resolution in Kubernetes
notetype : feed
date : 02-11-2021
---

To figure out how [[DNS Resolution]] works in [[Kubernetes]], there are a few important components to consider:
- k8s DNS server running on the cluster (e.g. [[CoreDNS]])
- Node's local DNS resolution (e.g. `/etc/resolv.conf`)
- [[Kubelet]] which creates pods and prepares them for DNS resolution
- [[Kubernetes Services]] which get cluster domain names in the k8s DNS server (e.g. `mysvc.default.svc.cluster.local`)

The question that we are interested in is how does a pod resolve a domain like `mysvc.default.svc.cluster.local` to the IP address that belongs to mysvc Service?

When a Service is created, CoreDNS creates a record to resolve it's hostname to it's IP address.

Your pod's dnsPolicy is set to `ClusterFirst`, which makes your pod use CoreDNS for DNS resolution. Based on this setting, when Kubelet creates your pod, it sets up appropriate rules in the pod (e.g. resolv.conf that points to the IP of CoreDNS). 

CoreDNS pod's policy is set to `Default`, so when Kubelet creates CoreDNS pods, it will make CoreDNS inherit the DNS resolution rules of the host node. This makes sure that CoreDNS will forward any non-cluster-dns requests to be resolved by the node itself - and Viola, you can resolve both `mysvc.default.svc.cluster.local` and `www.google.com` from your pod!

Instead of CoreDNS, it's possible to use anything that conforms with the [Kubernetes DNS Specification](https://github.com/kubernetes/dns/blob/master/docs/specification.md)

-----

Status: #🌱 

References:
- https://coredns.io/plugins/kubernetes/
