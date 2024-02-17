---
title : White Box Monitoring
notetype : feed
date : 28-05-2022
---

White Box [[Public/Monitoring]] is when we monitor the internal workings of our system. For example, users have no idea about our current CPU utilization, so that metric is a White Box metric. Its primary use is in collecting telemetry and debugging, but also has an important role in [[Alerting]] as well.

White Box Monitoring is useful for setting up strong [[Public/Cause Based Monitoring]], but it can also be used for [[Public/Symptom Based Monitoring]] in some cases as well, depending on who is looking at it and what data it shows.

When we look at internal metrics which are not directly visible to the user, we can gain insight into issues that are yet to come, and perform [[Alerting]] on them. For example, a user doesn't see that a disk is getting fuller, but they will get to feel it once it's completely full. When thinking about alerting on imminent issues, [[Public/Black Box Monitoring]] is a much better fit.

-----

Status: #💡 

References:
- [[Private/Book - Site Reliability Engineering]] ([Source](https://sre.google/sre-book/table-of-contents/))
- [[Public/Video - Practices for Creating Effective Customer SLOs]] ([Source](https://www.infoq.com/presentations/slo-pitfalls-2019/))

