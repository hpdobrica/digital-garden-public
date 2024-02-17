---
title : K8S Controller Manager
notetype : feed
date : 07-11-2021
---

Kube Controller Manager is a [[Public/K8S Master Node]] component that manages various controllers in [[Public/Kubernetes]]. Controllers are processes which continiously monitor the status of various parts of the cluster, and remediate the situation if that part of the cluster is not in its desired state.

Some of controllers which are part of controller manager are:
- [[Public/K8S Node Controller]]
- [[Public/K8S Replication Controller]]
- Deployment-Controller
- Namespace-Controller
- Endpoint-Controller
- Job-Controller
- CronJob
- PV-Protection-Controller
- PV-Binder-Controller
- Replicaset
- Replication-Controller
- ...

All of the controllers are packaged together into a process called `kube-controller-manager`. When you install Kubernetes Controller Manager, all of these controllers get installed as well.

-----

Status: #💡 

References:
- 
[]()