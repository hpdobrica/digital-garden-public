---
title : K8S Pod
notetype : feed
date : 07-11-2021
---

Pod is a [[Public/K8S Object]] used to run one or more tightly coupled containers and is rarely used directly, especially in production because of the limitations on the number of properties that can be updated. Instead, pods are usually managed by other objects like [[Public/K8S Replicaset]].

All containers in a pod can reach themselves via localhost as they are part of the same network. It's also easy to share volumes between them.

A pod can have a specific [[Public/K8S Service Account]] attached to it, otherwise it uses the default one.

-----

Status: #💡 

References:
- 
