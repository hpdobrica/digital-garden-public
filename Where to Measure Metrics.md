---
title : Where to Measure Metrics
notetype : feed
date : 29-05-2022
---

Different layers of infrastructure and application are exposing the same [[Monitoring]] metrics. For example, your database reports the query duration, and so does your application. These two are sure to have similar results – on application side, add a couple of milliseconds for latency and that's it.

Why the hell then would anyone want to collect some metric on application side if it's already provided by the database? The simplest answer is – if we don't have both, there is no way for us to tell if we are having a database issue, or a network issue.

As with everything else in engineering, [[Everything is a trade-off]], so let's look at some different places where you can measure something, and what are the pros and cons of each approach. For this example, let's say we are looking at [[Measuring Request Latency]].

#### Logs Processing

We could get the request latency by processing our application logs. 

This option is attractive when you are first starting out as it doesn't require changes to the application and allows you to backfill the request from the previous period.

However, the downside of this approach is coupling logs and metrics, as well as not being able to see the requests that didn't reach the application in the first place.

#### Application-exported Metrics

Using a tool like Prometheus, we can export our request latency as a metric. 

The good side of this approach it's very fast and cheap to add metrics in this fashion, and it gives us good flexibility of what our metrics will look like.

This approach also doesn't capture the requests that didn't manage to reach our service.

#### Infrastructure-exported Metrics

We could pick up metrics about request latency from our Load Balancer.

This is by far the easiest approach for getting started if you are in a cloud environment, as everything is prepared for you by default. This approach also captures the request much earlier in the chain and will also show requests which haven't reached the application (outside those which failed before reaching the load balancer, which is kind of out of our power anyway).

The downside of this approach is that we won't be able to measure more complicated requirements, and we are stuck with the metrics our load balancer exposes.

#### Synthetic Clients

Synthetic clients, also known as probers, are applications that send requests on a certain interval, and then validate and measure the responses.

The biggest advantage of using something like this is that they are able to measure all steps of complex user journeys, as their logic can be as complex as we want it to be.

The downside of using something like this is that the complexity of building and maintaining such clients is high. On the other hand, the more you do this, the more it edges towards end-to-end testing, which is not the place you want to go when thinking about monitoring.


#### Client Instrumentation

Client instrumentation is when we measure the user experience directly on the client side.

Since it's looking at data from a user's perspective, it's the most effective way to measure user experience.

Downside of this approach is that the measures taken on the client will take into account factors that depend on device and network the user is using, which is out of our scope as we can't act on them.


-----

Status: #💡 

References:
- [[Video - Practices for Creating Effective Customer SLOs]]
