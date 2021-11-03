---
title : K8S Apiserver
notetype : feed
date : 03-11-2021
---

Kube Apiserver is the primary component of a [[Kubernetes]] cluster. It runs on a Master Node, and is the only component which is talking directly to the [[etcd cluster]]. It exposes a REST API through which all K8S components interact with the cluster / with each other.

Whenever you execute a `kubectl` command, your client is sending a request to the Kube Apiserver.

If a `kubectl` GET request is sent, kube apiserver:
- authenticates and validates the request
- retrieves the data from etcd cluster
- responds back with the requested information

Instead of using `kubectl` it would be possible to invoke the APIs directly. For example, making a POST request to create a pod in the lines of `curl -X POST /api/v1/namespaces/default/pods....` will trigger the following actions:

- authenticate user
- validate request
- update etcd server
- inform the user that the Pod has been created

From here, other components start acting to make sure pod starts running. This process is described in more detail in [[What happens when you create a Pod in Kubernetes]].

-----

Status: #🌱 

