---
title : What should i be Alerting on
notetype : feed
date : 28-05-2022
---

When setting up [[Alerting]] for the first time, many people instinctively set alerts on [[Public/Cause Based Monitoring]] metrics – if my service's CPU is ramped to 100%, of course I want to be alerted! 

If someone asks "why is that so?", a simple answer is that such high CPU utilization results in a poor service performance, but this stance becomes much less important once you realize that:
- It's possible for your service to be slow while your CPU utilization is very low.
- It's possible for your service to be fast while your CPU utilization is very high.

Looking at these statements, we can make a good assumption that users don't actually care about our CPU utilization. 

As good [[Public/SLI]]s revolve around user experience, it's much better to look at [[Public/Symptom Based Monitoring]] when thinking about what metrics to set up [[Alerting]] on. 

Why not just measure the user experience directly, rather than try to look at all possible causes that can lead to issues?

In addition to this, there are also some [[Public/Cause Based Monitoring]] metrics that are useful to get alerts on – for example, for some things that aren't an issue right now, but are sure to become one in a short period of time. This would allow us to proactively act and negate the possible bad user experience. Make sure that alerts you set up with Cause Based Monitoring don't overlap with your Symptom Based Monitoring aalerts – inthis case, Cause Based alerts can be removed.


-----

Status: #💡 

References:
- [[Public/Video - Practices for Creating Effective Customer SLOs]] ([Source](https://www.infoq.com/presentations/slo-pitfalls-2019/))
