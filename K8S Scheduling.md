---
title : K8S Scheduling
notetype : feed
date : 03-11-2021
---

[[Public/K8S Scheduler]] is making sure that every [[Public/K8S Pod]] is assigned to a [[Public/K8S Node]]. Every pod that gets created has a property `NodeName` which is not set by default. kube-scheduler looks for pods with these fields unset and assigns them a node by setting the `NodeName` property.

The Pods are created before they are scheduled, and since the `NodeName` field is immutable, Scheduler can't just edit the pod. It has to create a [[K8S Binding Object]] and create a post request to the [[Public/K8S Apiserver]].

There are multiple constraints that scheduler needs to take into consideration while deciding where to place a pod:
- [[01 Inbox/K8S Resource Requests and Limits]]
- [[Public/K8S Node Selectors]]
- [[Public/K8S Node Affinity]]
- [[K8S Taints and Tolerations]]

If there were no kube-scheduler on the cluster, you could create the pod with the `NodeName` already set. 

-----

Status: #💡 

