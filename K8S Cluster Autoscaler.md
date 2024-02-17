---
title : K8S Cluster Autoscaler
notetype : feed
date : 09-01-2023
---

[[Kubernetes]] Cluster Autoscaler represents one of the types of [[Kubernetes Autoscaling]].

Its job is to add or remove [[K8S Node]] based on cluster usage. It works by checking for [[K8S Pod]]s that are `Pending` [[K8S Scheduling]], and creates new Nodes if this is due to insufficient cluster capacity. It also tries to pack existing pods onto fewer nodes in an effort to destroy nodes which can be destroyed.

By default, Cluster Autoscaler checks for pending pods every 10 seconds, but this is configurable via `--scan-interval` flag.

It's worth noting that Cluster Autoscaler doesn't take CPU and memory utilization when making its decisions, but only [[01 Inbox/K8S Resource Requests and Limits]]. Because of this, it has no idea how much of requested resources is actually used, which could lead to scaling up an already overprovisioned cluster if we are not paying attention.



-----

Status: #💡 

References:
-  [Kubecost - Kubernetes Cluster Autoscaler](https://www.kubecost.com/kubernetes-autoscaling/kubernetes-cluster-autoscaler/)
