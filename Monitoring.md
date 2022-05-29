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


Efficient monitoring systems are best achieved with heavy use of [[White Box Monitoring]] with a bit of [[Black Box Monitoring]].  In addition to this, it's very important for efficient monitoring systems to be able to tell what ([[Symptom Based Monitoring]]) from why ([[Cause Based Monitoring]]). 


Don't shy off from recording "the same metric" in different places – see [[Where to Measure Metrics]].






-----

Status: #💡 

References:
- [[Book - Site Reliability Engineering]]
- [[Video - Practices for Creating Effective Customer SLOs]]
- 
