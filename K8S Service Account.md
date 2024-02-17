---
title : K8S Service Account
notetype : feed
date : 07-11-2021
---

Service Accounts are [[K8S Object]]s used to help pods with [[K8S Authentication]].

The ServiceAccount object is namespace-scoped. It's used to allow a process in a pod to access Kubernetes API Server. There exists a default service account object, but it has no permissions attached to it.

When a new Service Account is created, proper access should be given through [[K8S RBAC]]. The service account can then be used to obtain auth token and CA certificate to authenticate to [[K8S Apiserver]]. This information is held inside a [[K8S Secret]] which is automatically created together with Service Account. 

> The secret is automatically mounted inside `/var/run/secrets/kubernetes.io/serviceaccount/`. This behavior can be disabled by setting `automountServiceAccountToken` to `false`.


The service account can be imperatively created with `kubectl create serviceaccount myserviceaccount`.

-----

Status: #💡 

References:
- 
