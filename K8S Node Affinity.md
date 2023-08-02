---
title : K8S Node Affinity
notetype : feed
date : 24-12-2021
---

Node Affinity is a feature which ensures that [[K8S Pod]] end up running on specific [[K8S Node]]. We are already able to do this with [[K8S Node Selectors]], but with big limitations.

See also [[K8S Anti-affinity]] if you need to set affinity based on running pods and their labes instead.

If we take the node selector example of making a pod run on a specific node like this:

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

Doing the same thing with Node Affinity looks like this:

```yaml

apiVersion: v1
kind: Pod
metadata:
  name: some-pod
spec:
  containers:
    - name: some-name
      image: some-image
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
          - matchExpressions:
            - key: Size
              operator: In
              values:
                - Large

```


## Match Expressions

If you want your pod to be placed on `Large` or `Medium` Node, you can just add `Medium` to the list of values.

Assuming `Small`, `Medium` and `Large` Nodes, you could do the same thing by specifying:

```yaml

 - key: Size
   operator: NotIn
   values:
     - Small

```

If you dont care what value is of the label, only that the label exists, you can use `Exists` operator with no values instead.

There are more operators described in the k8s docs.

## Node Affinity Types

`requiredDuringSchedulingIgnoredDuringExecution` - this sentence-like property describes the type of Node Affinity that we are defining. These types define the behavior of the k8s scheduler.

These are the available affinity types:

-   `requiredDuringSchedulingIgnoredDuringExecution`
-   `preferredDuringSchedulingIgnoredDuringExecution`

These are not available yet but planned for the future:

-   `requiredDuringSchedulingRequiredDuringExecution`
    

As you can see, there are two states in the lifecycle of a pod when considering Node Affinity - **DuringScheduling** and **DuringExecution**.

DuringScheduling is where a pod does not exist and is created for the first time. If you set the DuringScheduling to Required, it makes sure that when scheduling this new Pod, rules specified below are required to be fulfilled - the pod will be placed on a node with this label, or will not be placed at all. Selecting PreferredDuringScheduling instead will schedule the pod on some other nodes if it can't schedule it on the node we requested.

DuringExecution is a state where a pod has been running, but a change in the environment has been made that affects Node Affinity. Let's say the label gets removed from the Node while the pods are alredy running on it with the node affinity which depends on this label. Currently the only option for this is **Ignored**, which means that any changes that affect node affinity will not affect already running pods. In the future when we get the **Required** option as well, we will use it to make sure the pods that no longer fulfill the criteria on a given node actually get evicted.

-----

Status: #🌲 

