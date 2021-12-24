---
title : K8S Node Selectors
notetype : feed
date : 24-12-2021
---

Node Selectors are used to place [[K8S Pod]]s on specific Node by label. For more complex placement options, see [[K8S Node Affinity]].

It's possible to make a pod go to a specific node based on the node label. For example, if you have one large node and two smaller nodes, and you have a workload which needs to run on the large node, you can make it run there by specifying:

```yaml

apiVersion: v1
kind: Pod
metadata:
  name: some-pod
spec:
  containers:
    - name: some-name
      image: some-image
  nodeSelector:
    size: Large


```

In order for this to work, we need to label the large node with `size: Large`. We can do this by running:

```bash
kubectl label nodes <node-name> <label-key>=<label-value>
```


-----

Status: #🌲 

