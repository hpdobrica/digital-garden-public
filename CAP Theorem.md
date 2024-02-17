---
title : CAP Theorem
notetype : feed
date : 11-08-2022
---

CAP theorem states that distributed data stores can provide only two of the Consistency or Availability and Partition Tolerance. Since network failures are unavoidable, we can assume that Partition Tolerance is something we need to have. CAP theorem states that we can provide either consistency or availability during a network failure - never both.

CAP stands for:
- `C`onsistency
- `A`vailability
- `P`artition Tolerance

## Consistency

In essence, in order for [[Public/Database]] to be consistent, it must always respond to requests with either latest data, or with errors.

In order for strong consistency to happen in a [[Distributed System]], the update must be applied to all nodes at the same time (This means that read replicas are not strongly consistent - special logic is needed to handle replication lag).

It's understood that instant, global consistency is not possible, so the goal of consistency is to push the time needed for database to become consistent to a point that it's not noticeable.

## Availability

Availability means that every received request is responded with the expected data (non-error response except when an error is expected). 

As we know from [[Public/Service Availability Target]]s, 100% availability is very hard and expensive to reach - if you have the same data stored on 5 nodes, and all 5 nodes fail at the same time, your request won't be able to be served, and you are paying a lot for these 5 nodes.

If we have nodes which are 99.9% available, the more nodes we have, the higher the chance some of them will fail (with 40 nodes this drops to about 96% if we ignore that the failures usually arent isolated and can cascade).

## Partition Tolerance

Since [[Public/Network Partition]]s are pretty much unavoidable, especially in distributed systems, Partititon Tolerance means that a distributed system is able to continue operating even though some of its components can't communicate or are unavailable.


## The Tradeoff

So, in the inevitable event of failure, we need to ask ourselves if we are going to sacrifice consistency or availability.

[[Public/Yield and Harvest]] are good metrics to consider in a system which makes trade-offs like this.

### Consistency over Availability

This means that in the event of partial failure, our distributed system will guarantee the atomicity of reads and writes by refusing to respond to some requests.

The system might decide to completely shut down, refuse new writes, or only respond to requests served from within a partition where master node is.

This is a reasonable choice for any system that has a hard requirement on consistency.

### Availability over Consistency

This means that in the event of partial failure, our distributed system will respond to all requests the best it can, potentially serving stale data or accepting conflicting writes, which are later often resolved via causal ordering mechanisms (e.g. vector clock), or application-specific conflict resolution procedures. 


This is a reasonable choice for any system which can to some extent tolerate stale data and is capable of conflict resolution - especially when availability is crucial.



-----

Status: #💡 

References:
- [You Can’t Sacrifice Partition Tolerance](https://codahale.com/you-cant-sacrifice-partition-tolerance/)
