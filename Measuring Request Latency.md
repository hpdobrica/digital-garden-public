---
title : Measuring Request Latency
notetype : feed
date : 29-05-2022
---


Latency is the time taken to serve a request, and is one of [[The Four Golden Signals of Monitoring]].

The most common metric looked at here is usually the [[Mean]] latency, but this can easily become misleading – imagine serving 99 requests in 10ms and serving one in 20000ms gives you an average latency of ~210ms which is not a good representative of what's actually happening.

A cheap and easy alternative to this would be to use a (e.g. [[Prometheus]]) Histogram metric and store request in buckets based on their latency (requests that completed in 0-10ms, 10-30ms, 30-100ms, +100ms). With the same set of requests, this would give us a much more precise idea about what's going on (99 requests of 0-10ms and 1 request of +100ms). The buckets can be configured around our [[SLO]]s so that we can easily track how we are standing.

Taking the same bucket idea a step further would be to utilize the same data to calculate [[Percentile]]s of response times – be careful however to understand the following:
- When using Histograms, response times in percentiles are estimated – you are guaranteed the value to be from the correct bucket, but the value itself is calculated via [[Linear Interpolation]]
- the more buckets you have and the smaller they are, the more precise the value in the percentile will be
- this however costs a lot as more buckets == higher metric cardinality, which we want to avoid if we want to have monitoring system that's actually usable

In addition to tracking your response times, it's valuable to distinguish between latency of failed and successful requests, as the errors can skew the image of what our response times look like.  Imagine having a lot of errors that fail early on and show you that your response times are much faster than they normally are.

On the other hand, you should also track error latency itself to see how slow your error responses are, so you can make sure you are [[Failing Fast]].


-----

Status: #💡 

References:
- [[Book - Site Reliability Engineering]] ([Source](https://sre.google/sre-book/table-of-contents/))
- [Prometheus Docs – Histograms and Summaries](https://prometheus.io/docs/practices/histograms/)
