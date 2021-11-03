---
title : What happens when you create a Pod in Kubernetes
notetype : feed
date : 03-11-2021
---

Once you run `kubectl run busybox --image busybox` on your [[Kubernetes]] cluster, what has to happen before your [[K8S Pod]] is running successfully?

The [[K8S Apiserver]] is the component which recieves your request, authenticates you, validates the request and writes your action into [[etcd cluster]]. At this point, the pod resource is created, but is in Pending state.

[[K8S Scheduler]] is continuously monitoring the Apiserver for pods that require scheduling. Once it notices our pod is not assigned to a Node, it will identify the node where the pod will be placed, and will inform Apiserver about this decision. This process is described in more detail in [[K8S Scheduling]].

Once Apiserver recieves the request from scheduler, it updates the etcd cluster and passes this information over to the [[Kubelet]] of the appropriate worker node.

The kubelet will then:

- create the pod on the node
- instruct the container runtime engine ([[K8S CRI]]) to deploy the application image
- invoke the [[K8S CNI]] plugin to add the new pod to the pod network
- configure DNS resolution in that pod so it can reach the services and pods by their domain names ([[DNS Resolution in Kubernetes]])
- update the status back to the Apiserver, who lastly updates the data again into the etcd cluster

At this point, your Pod is successfully running on a Node.
 

-----

Status: #🌱 