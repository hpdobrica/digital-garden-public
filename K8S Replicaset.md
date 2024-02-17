---
title : K8S Replicaset
notetype : feed
date : 07-11-2021
---

ReplicaSets are [[K8S Object]]s used to make sure a certain number of [[K8S Pod]]s is running on the Kubernetes cluster.

ReplicaSet uses the labels defined in the selector property to find all the pods with the specified labels. Once it finds them, it makes sure that the number of existing pods matches the number of pods requested via `replicas` property.

If the number of pods is less than specified, it uses the provided template to create a new pod. If this pod has the labels that match the ones specified in selector, it will take this new pod into consideration when counting again.


> ReplicaSet doesn't just manage pods that it creates, it manages all pods with a given label, no matter the source.

The actual process performing this work is [[K8S Replication Controller]].

ReplicaSet can be a target of [[K8S Horizontal Pod Autoscalers]].

-----

Status: #💡

References:
- https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/
