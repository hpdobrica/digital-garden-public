---
title : Elasticsearch Quorum
notetype : feed
date : 22-01-2023
---

In [[Elasticsearch]], modification of cluster state and master node election can only be performed by master nodes. In order to allow for some fault tolerance of the cluster, each decision is made through a quorum of eligible master nodes by getting a confirmation from the majority of masters.

As nodes get added and removed, Elasticsearch automatically updates its voting configuration to know how many nodes need to confirm the action before it's considered successful. This process takes a short amount of time, but it's important to let it complete for each node before adding/removing any additional nodes.

You need to be careful to never have more than half of the master eligible nodes unavailable, as it will lead to the cluster being unusable.

Systems that work like this favor having an uneven number of nodes because it enables it to determine majority and avoid "split-brain" problem where [[Network Partition]] ends up creating two equally sized halves of the cluster which both believe they have the majority. To overcome this, when you have an even number of masters, Elasticsearch will ensure that  one of them doesn't take part in decision making. 

Master election happens on cluster startup and in case an elected master fails.

If multiple masters are taken down and quorum is lost, but they are quickly taken back online (as during a [[Rolling Update Deployment Strategy]]), Elasticsearch will recover on its own. This will happen without issues, as the existing set of masters that are already part of the voting configuration will remain unchanged after the masters are back up.

For the first election, Elasticsearch needs to rely on an externally-provided set of master eligible nodes, which can be provided in the configuration through `cluster.initial_master_nodes`.

You can see the list of nodes that are part of the current voting configuration by querying:
```bash
curl -XGET https://localhost:9200/_cluster/state?filter_path=metadata.cluster_coordination.last_committed_config
```


-----

Status: #🌱 

References:
- [Elasticsearch Docs - Discovery and cluster formation](https://www.elastic.co/guide/en/elasticsearch/reference/current/modules-discovery.html)