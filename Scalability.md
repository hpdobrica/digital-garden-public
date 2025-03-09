---
title: Scalability
notetype: feed
date: 04-02-2025
---
A scalable system is a system that can deal with increasing growth (of data, traffic, complexity) in a reasonable ways.

We can never just say that a system is or isn't scalable. The right way to think about scalability is in terms of questions like "if a system grows in this particular way, what are our options for dealing with that growth?". This is because the problematic part of the system may be the volume of reads, the volume of writes, the volume of data to store, the complexity of the data, the response time requirements, the access patterns, or (usually) some mixture of all of these plus many more issues.

Before thinking of how to scale, we must first understand system's load parameters that allow us to quantify the load - requests per second, read/write ratio, number of active users, cache hit rate, distribution of followers per user (e.g. twitter).

Once we know what the load on our system is, we can start thinking about what happens when that load increases and our resources stay the same. How does this affect performance of our system? With a given load increase, how much do we need to bump up resources in order for performance to stay unchanged?

Another question that this raises is how do we define and measure performance? Depending on the type of the system, we might care more about throughput (asynchronous job processing), or about  [[Measuring Request Latency|Request Latency]] (online services).

## Scaling

When it comes to increasing resources, there is often a choice between:
- Scaling Up (vertical scaling, moving to a more powerful machine) 
- Scaling Out (horizontal scaling, distributing load across multiple smaller machines)

Scaling up is often simpler as the software that can run on a single machine is simpler and easier to maintain, but moving to bigger and bigger machines can become expensive very quickly.

On the other hand, scaling out brings its set of issues to the table, as distributed systems have to care about stuff like [[Consensus]].

Some systems are elastic, meaning that they can automatically add computing resources when they detect a load increase, which is especially important if the load on the system is unpredictable.

-----

Status: #📥

References:
- [[Book - Designing Data Intensive Applications]] ([Source](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321))
