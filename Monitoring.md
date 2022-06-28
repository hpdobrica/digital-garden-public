---
title : Monitoring
notetype : feed
date : 21-05-2022
---

When I was working as a developer on the first application that was actually running in production, we relied on looking at the application logs to figure out if something is wrong. We did it for a long time, and we were as proficient in it as one can get. 

I was routinely checking the logs for errors, when I noticed that something is off – in the postmortem, a smart man told me "logs should be the last place you should have to look when faced with an issue like this". This sentence seemed a bit absurd to me at the time – what do you mean, where am I supposed to look instead? Needless to say, back then, I knew nothing about monitoring.

Monitoring is an integral part of running services in production. Without it, we are blind to what's going on, and thus unable to act according to our best interest.

Providing visibility is in the center of monitoring, but speaking more broadly, monitoring allows us to:
- easily debug our systems
- see how a change impacts our system
- implement [[Alerting]] that something is broken or will break soon
- perform long-term trend analysis


In essence, monitoring is collection of events and their contexts (e.g., HTTP request is an event, its full context holds all details about it: url, body, status code...). Ideally, we'd have all events together with their whole contexts. In reality, that's a lot of data, so we need to divide monitoring into four categories based on how we collect the data:
- [[Profiling]]
- [[Tracing]]
- [[Logging]]
- Metric Monitoring

## Metric Monitoring

Metric Monitoring (often refered to as just monitoring) is a type of Monitoring which gives up on event context to provide event information over time. It's a system that focuses on overall system health and behavior - not on individual events.

Although metrics rely on having little context to function (too much context == too big metrics), we sometimes want to add some context to our metrics (e.g. path of the http request). We need to be careful because now each path our application has would now count as another metric.

Tracking user emails would be a bad idea as it's unbounded cardinality - each email would create a new number for us to track (not to mention that emails are personally identifiable information, which have no place in metrics).

As a general rule of thumb, no process should ever track more than 10000 distinct numbers.

When debugging an issue, Metrics can show you in which system the slowdown is, while [[Logging]] can help you pinpoint where in that system it's occuring

Efficient metric monitoring systems are best achieved with heavy use of [[White Box Monitoring]] with a bit of [[Black Box Monitoring]].  It's very important for efficient monitoring systems to be able to tell what ([[Symptom Based Monitoring]]) from why ([[Cause Based Monitoring]]), as this will have a large impact on how we actually use the metrics we collect. 

[[The Four Golden Signals of Metric Monitoring]] is a good place to start figuring out what to have on your service dashboards.

Don't shy off from recording "the same metric" in different places – see [[Where to Collect Metrics]].



-----

Status: #💡 

References:
- [[Book - Site Reliability Engineering]]
- [[Video - Practices for Creating Effective Customer SLOs]]
- 
