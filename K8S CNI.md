---
title : K8S CNI
notetype : feed
date : 03-11-2021
---

[[Public/Kubernetes]] implements CNI(Container Network Interface) to allow third-party networking solutions to integrate with it.

Each CNI solution needs to implement a set of things including, but not limited to:
- creating bridge networks
- attaching containers to them
- assigning IP addresses to containers
- port forwarding

Kubernetes comes with a set of CNI plugins supported by default (`BRIDGE`, `VLAN`, `IPVLAN`, `MACVLAN`, `WINDOWS`). In addition to this, there are third-party plugins like `Flannel`, `WeaveWorks` and `Cilium`.

[[Public/Docker Networking]] does not support CNI standard, so when Docker is used in kubernetes, containers must be created with `--network none` option in order to let the CNI plugin manage network for them.

-----

Status: #💡 

