---
title : White Box Monitoring
notetype : feed
date : 28-05-2022
---

White Box [[Monitoring]] is when we monitor the internal workings of our system. For example, users have no idea about our current CPU utilization, so that metric is a White Box metric. Its primary use is in collecting telemetry and debugging, but also has an important role in [[Alerting]] as well.

White Box Monitoring is useful for setting up strong [[Cause Based Monitoring]], but it can also be used for [[Symptom Based Monitoring]] in some cases as well, depending on who is looking at it and what data it shows.

When we look at internal metrics which are not directly visible to the user, we can gain insight into issues that are yet to come, and perform [[Alerting]] on them. For example, a user doesn't see that a disk is getting fuller, but they will get to feel it once it's completely full. When thinking about alerting on imminent issues, [[Black Box Monitoring]] is a much better fit.

-----

Status: #💡 

References:
- [[Book - Site Reliability Engineering]]
- [[Video - Stop Talking & Listen; Practices for Creating Effective Customer SLOs]]
