---
title : Cause Based Monitoring
notetype : feed
date : 28-05-2022
---

Cause Based [[Public/Monitoring]] points us to a cause of an existing issue, but don't imply that issue exists in the first place. Some examples of Cause Metrics are:
- CPU utilization
- Free disk space

When users are seeing slow response times, I want to be able to easily tell that it's because our DB server is running close to 100% CPU utilization – this should be the primary use of Cause Based Monitoring. 

On the other hand, Cause Metrics are only in rare cases useful in [[Alerting]]. See [[Public/What should i be Alerting on]].



-----

Status: #🌱 

References:
- [[Public/Video - Practices for Creating Effective Customer SLOs]] ([Source](https://www.infoq.com/presentations/slo-pitfalls-2019/))
