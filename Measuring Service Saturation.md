---
title : Measuring Service Saturation
notetype : feed
date : 29-05-2022
---

Saturation is a representation of how full your service is, and is one of [[The Four Golden Signals of Monitoring]]. 

When thinking about saturation, it's useful to put the emphasis on the most constrained resource for your application – If memory is our biggest constraint, our dashboards should show our service's memory usage.

Saturation is useful because performance degradation often starts before saturation reaches 100%, so it's important to define a utilization target which you'd like to follow.

Increases in [[Measuring Request Latency]] are frequently leading indicators of high saturation, so it's good to supplement Saturation metrics with high-level latency metrics.

Saturation also cares about things like "your hard drive will be full in 4h". 

It's critical to note that Saturation almost always falls under [[Cause Based Monitoring]], so make sure not to rely on it too hard when setting up [[Alerting]].



-----

Status: #💡 

References:
- [[Private/Book - Site Reliability Engineering]] ([Source](https://sre.google/sre-book/table-of-contents/))
