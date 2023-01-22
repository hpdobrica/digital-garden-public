---
title : Elasticsearch
notetype : feed
date : 17-01-2023
---

Elasticsearch is a distributed search and analytics engine that serves as a data/document store in Elastic Stack.

It stores data in serialized JSON documents which are indexed inside an inverted index data structure to provide very quick lookups. Indexing is done based on a schema, but this schema can be dynamically determined based on the format of provided documents (as long as provided data types are consistent).

Scalability and resilience comes from the fact that Elasticsearch is a distributed data store which consists of multiple nodes. Query load is distributed between the nodes for faster processing, and data is automatically redistributed to ensure no node is heavier and under more load than the others.

## Indices and Shards

To make data more portable, indices are split into "primary" shards (which themselves act as a standalone indices), and the shards are then distributed across nodes. The number of shards an index has is determined at index creation time, and cannot be changed later as it would influence the underlying hashing algorithm which determines the location of data across shards.

In addition to primary shards, there also exist secondary shards which are just replicas of primary shards, so their number can be changed after index creation.

Determining an optimal number and size of the shards is an important decision in managing Elasticsearch clusters:
- having many smaller shards increases the overhead of index maintenance cluster has to perform
- having a smaller number of bigger shards means that the shards will be harder to move around when rebalancing needs to happen

A rule of thumb for how large shards should be is between ten and multiple tens of gigabytes. It's pretty common to see shards which are 20-40 GB in size.

## Resilience

To ensure good performance, nodes of the cluster should be close to each other and have good connection between them. To allow for this and still guard ourselves from regional failures, we can make use of Cross-Cluster Replication, which can create a hot failover read replica which can take over in an event of primary region failure.



-----

Status: #🌱 

References:
- [Elasticsearch Docs - Intro](https://www.elastic.co/guide/en/elasticsearch/reference/current/elasticsearch-intro.html)
