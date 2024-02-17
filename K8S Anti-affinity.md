---
title : K8S Inter-pod Affinity / Anti-affinity
notetype : feed
date : 23-12-2021
---

While [[K8S Node Affinity]] works like an extended [[K8S Node Selectors]], Inter-pod affinity and Anti-affinity focus on labels of the pods rather than labels of the [[K8S Node]].

This allows us to dictate which pods can or can't be deployed together on the same node.

Example inter-pod affinity rule might sound like: `This pod should run on this part of infrastructure, if this part of infrastructure is already running some pods that meet the specified criteria`.

Similarily, anti-affinity rule could be read in the lines of: `This pod should not run on this part of infrastructure, if this part of infrastructure is already running one or more pods that meet the specified criteria`.

## Topology key

When I say `This part of infrastructure`, it could mean any node or group of nodes, based on a specific label. The rule could set limits:
- on a single node
- on one of nodes in a single cloud provider region / availability zone
- any other label available on your nodes

To determine the part of the infrastructure which will be taken into consideration for these rules, we use `topologyKey` property. Topology key represents a key of any label that is present on all of your nodes (if some nodes are missing this label it could cause issues).

For example, setting `topologyKey` to `kubernetes.io/hostname` will turn the `this part of infrastructure` into `this node` in the example above, as each node will have a distinct label for the hostname.

Setting `topologyKey` to something like `topology.kubernetes.io/zone` will turn the `this part of infrastructure` into `any node in this zone` in the example above, as each node will have a distinct label for the hostname.

## Practical example

The full example below demonstrates both the anti affinity (`podAntiAffinity` key) and the inter-pod affinity (`podAffinity` key).

First rule says that our [[K8S Deployment]] should run on any given node (`topologyKey: "kubernetes.io/hostname"`) only if there are no other [[K8S Pod]]s with label `app: web-store` already running on it. This stops our deployment's pods to be co-located on a single node (in a way similar to [[K8S DaemonSet]], just with specific number of replicas).

Second rule says that our deployment's pods should run only on nodes where pods with label `app: store` are already running.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: web-server
spec:
  selector:
    matchLabels:
      app: web-store
  replicas: 3
  template:
    metadata:
      labels:
        app: web-store
    spec:
      affinity:
        podAntiAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
          - labelSelector:
              matchExpressions:
              - key: app
                operator: In
                values:
                - web-store
            topologyKey: "kubernetes.io/hostname"
        podAffinity:
          requiredDuringSchedulingIgnoredDuringExecution:
          - labelSelector:
              matchExpressions:
              - key: app
                operator: In
                values:
                - store
            topologyKey: "kubernetes.io/hostname"
      containers:
      - name: web-app
        image: nginx:1.16-alpine
```


-----

Status: #🌲 

References:
- [K8S Docs](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity)