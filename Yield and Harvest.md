---
title : Yield and Harvest
notetype : feed
date : 11-08-2022
---

When designing distributed systems and talking about their consistency and availability, Yield and Harvest are two terms/metrics we can utilize to get a better understanding of how our system behaves, and which tradeoffs we are making

## Yield

Yield is pretty similar to uptime, but for each second of downtime, yield asks how important it was, instead just taking it at face value.

If we were down for one second, and no requests were sent to us during this time, this has an impact on our uptime, but not an impact on our yield.

On the other hand, if during this second we were supposed to serve some requests, both our uptime and yield will go down.

Since it's very critical whether that second happened during peak time or when no one was around, yield is a much better metric to track than the uptime.

## Harvest

Harvest is a metric which shows which portion of the total requested data available was served with a request. It's a very significant metric when considering consistency/availability tradeoff in [[Public/CAP Theorem]].

If we have 3 nodes, each holding 3 pieces of requested data, and one of the nodes was unavailable during request time - we could only respond with two pieces of data, so the harvest for this request would be 66%.

Another example of below-100% harvest is a system which stores older versions of documents, and decides to serve not-the-most-recent document because it's better to serve that than to serve nothing.


-----

Status: #🌱 

References:
- [You Can’t Sacrifice Partition Tolerance](https://codahale.com/you-cant-sacrifice-partition-tolerance/)
