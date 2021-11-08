---
title : K8S Node Controller
notetype : feed
date : 07-11-2021
---

Node Controller is responsible for monitoring the status of the nodes in [[Kubernetes MOC]] cluster and keeping them in the desired state. It does this through the [[K8S Apiserver]]. 

This is the workflow by which Node Controller works:
- If a new node is created, Node Controller will assign it a [[CIDR]] block.
- it checks the status of the nodes every 5 seconds
- if it stops receiving heartbeat from a node, that node is marked as unreachable after the grace period of 40 seconds
- after it's marked unreachable, it has 5 minutes to come back up
- if it doesn't, pods get evicted from that node, and get provisioned to the healthy ones (if they are a part of a [[K8S Replicaset]])

-----

Status: #🌱 

References:
- https://kubernetes.io/docs/concepts/architecture/nodes/#node-controller
