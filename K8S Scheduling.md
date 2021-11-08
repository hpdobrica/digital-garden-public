---
title : K8S Scheduling
notetype : feed
date : 03-11-2021
---

[[K8S Scheduler]] is making sure that every [[K8S Pod]] is assigned to a node. Every pod that gets created has a property `NodeName` which is not set by default. kube-scheduler looks for pods with these fields unset and assigns them a node by setting the `NodeName` property.

The Pods are created before they are scheduled, and since the `NodeName` field is immutable, Scheduler can't just edit the pod. It has to create a [[K8S Binding Object]] and create a post request to the [[K8S Apiserver]].

There are multiple constraints that scheduler needs to take into consideration while deciding where to place a pod:
- [[K8S Resource requirements and Limits]]
- [[K8S Node Selectors]]
- [[K8S Node Affinity]]
- [[K8S Taints and Tolerations]]

If there were no kube-scheduler on the cluster, you could create the pod with the `NodeName` already set. 

-----

Status: #💡 

