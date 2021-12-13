---
title : K8S Static Pod
notetype : feed
date : 13-12-2021
---

Static pods are [[K8S Pod]]s run solely by [[Kubelet]] without any interference from kube-apiserver and other controlplane components.

Kubelet uses `/etc/kubernetes/manifests` directory to host static pod manifests by default (directory is configurable in kubelet config). Any pod manifests that are put in this directory, wiill be started by kubelet on its node.

You can tell that a pod is static when looking at a list of pods, because it will always have a node name appended to it.

Static pods are especially important when cluster is set up the kubeadm way, because most [[K8S Master Node]] components and [[etcd cluster]] actually run as static pods.

-----

Status: #🌱 

References:
- 
