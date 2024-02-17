---
title : Black Box Monitoring
notetype : feed
date : 28-05-2022
---

Black Box Monitoring is when we look at our system from the perspective of our users – without knowing anything about its internal state.

Since Black Box Monitoring is looking at customer experience, it can show us any currently active problems (e.g., high error rate, slow response times), but it's fairly useless at predicting the soon-to-happen problems – for this we need to use [[White Box Monitoring]].

For [[Alerting]], Black Box Monitoring has a key benefit of being able to warn us only when an issue is contributing to the real symptoms ([[Symptom Based Monitoring]]).

-----

Status: #💡 

References:
- [[Private/Book - Site Reliability Engineering]] ([Source](https://sre.google/sre-book/table-of-contents/))
- [[Video - Practices for Creating Effective Customer SLOs]] ([Source](https://www.infoq.com/presentations/slo-pitfalls-2019/))