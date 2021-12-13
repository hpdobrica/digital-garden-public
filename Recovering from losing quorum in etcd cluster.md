---
title : Recovering from losing quorum in etcd cluster
notetype : feed
date : 13-12-2021
---

In case you are running a [[Kubernetes]] cluster in a HA setup with say, 3 [[K8S Master Node]]s, loss of majority of the nodes will stop the cluster from reaching [[Consensus]] and thus, from functoning. 

The main reason this breaks tha HA cluster is that [[etcd cluster]] loses ability to establish quorum between its members. Even though 2/3 members are dead, if they are not explicitly removed by `etcdctl member remove`, the remaining node will still try to reach them. 

This is a problem, but luckily all we need to do is remove the dead members, right? Right? 

Well, if the etcd cluster can't elect a leader, you can't ever run `etcdctl member list` against it. The cluster is stuck in leader election and doesn't care about your input.

The way you can get out of this mess is thankfully pretty simple. You just need to add `--force-new-cluster` flag to etcd command (inside of [[Kubelet]]'s [[K8S Static Pod]] manifest), which will initialize a new single-node etcd cluster and removes the dead members. 

After this is done, you just need to add the rest of the nodes to this new cluster with `etcdctl member add` or `kubeadm join phase control-plane-join etcd --control-plane` if you are using kubeadm.

-----

Status: #🌱 


