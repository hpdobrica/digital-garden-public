---
title : K8S Worker Node
notetype : feed
date : 07-11-2021
---

Worker nodes are the place where the actual work is being executed inside k8s cluster. They run workloads as dictated by the [[K8S Master Node]], and update the master node on their status so it can manage them.

These are the main components of the worker node:
- kubelet - agent which runs on each node. listens for instructions from apiserver, provides status reports to apiserver. deploys/destroys containers as requested
- kube-proxy - allows containers running on nodes to reach each other
- container runtime - e.g. [[Docker]]

-----

Status: #📥

References:
- 
