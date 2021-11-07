---
title : K8S Object
notetype : feed
date : 07-11-2021
---

To see a list of available [[Kubernetes]] objects on your cluster, you can run:

```bash

# all
kubectl api-resources

# only namespaced
kubectl api-resources --namespaced=true

# only cluster-scoped
kubectl api-resources --namespaced=false

```

-----

Status: #🌱 
