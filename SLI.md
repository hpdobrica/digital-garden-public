---
title : SLI
notetype : feed
date : 08-01-2022
---

Service Level Indicators are quantitative measures of provided level of service, often aggregated into rates, averages, percentiles. 

Common SLIs are availability, error rate, latency, throughput, durability of data.

We have a lot of metrics we are [[Public/Monitoring]] in our systems, but not all of them should be defined as SLIs.  Good SLIs are metrics that our users care about. When we don't have the metrics our users care about the most (e.g. frontend latency), we should find the next best thing that we have available (e.g. backend latency).

If in some cases server-side metrics (e.g. gathered via [[Public/Prometheus]] or log processing) are not good enough, measuring frontend metrics (e.g. time to a full page load) can give us much more information and cover some potential blind spots (e.g. slow js on frontend).

Having too many SLIs defined is guaranteed to cause problems, as you can't possibly pay attention to everything all the time. On the other hand, having too few SLIs could leave big holes in the behavior of your system.

When deciding which indicators to choose, its better to start from desired [[Public/SLO]]s and work your way back to indicators. See [[Public/Defining Service Level Objectives]].

When aggregating metrics for SLIs its much better to use percentiles than the [[Public/Mean]], as mean can hide many things we'd be interested in - if most requests complete within 50ms, but 5% of requests are 20x slower, it'd be hard to notice such a thing on mean chart.




-----

Status: #💡 
References:
- [[Private/Book - Site Reliability Engineering]] ([Source](https://sre.google/sre-book/table-of-contents/))
