---
title : Kubelet
notetype : feed
date : 03-11-2021
---

Kubelet runs on a [[Public/Kubernetes]] node and is responsible for managing the node it's runnning on. It starts and stops nodes as requested by the [[Public/K8S Apiserver]]. It also updates the kube apiserver on the worker node status in regular intervals.

Kubelet registers the node with the kubernetes cluster. When it recieves the request to run a pod/container from [[Public/K8S Scheduler]], it sends the request to container runtime to pull the required image and run an instance. Kubelet then monitors the state of the pod and containers within it and reports their state to the [[Public/K8S Apiserver]].

Regardless of the way cluster is set up, Kubelet is always manually installed and should be running as a service. 

You can easily find its configuration by inspectig the running process:

```bash
ps -aux | grep kubelet
```

-----

Status: #💡 

References:
- 
