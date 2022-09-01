---
title : Network Partition
notetype : feed
date : 11-08-2022
---

Network Partition is a division of a network into a separate subnets, either by design or by network failure. 

When a network partition occurs, all traffic sent from a component in partition A to components in partition B will be lost. Any pattern of message loss can be modeled as a temporary network partition, lasting long enough for the message in question to be lost.

Network partitions can't be experienced only by single-node, monolythic systems. Even in case of systems like these, network partition can happen between the monolith and its client, still causing a problem.

The cause of Network Partition is not just dropping packets - even when a node crash occurs, it can be said that the network was partitioned in two pieces - failed node, and the rest of the network.

-----

Status: #🌱 

References:
- [You Can’t Sacrifice Partition Tolerance](https://codahale.com/you-cant-sacrifice-partition-tolerance/)
