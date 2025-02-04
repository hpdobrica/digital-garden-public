---
title : Service Reliability
notetype : feed
date : 08-01-2022
---

A reliable system is a system that continues to work correctly at the desired level of performance even when faced with issues like hardware [[Fault]]s, software [[Fault]]s and human errors.



Reliability of services is crucial in most applications, and everyone should aim for their services to be reliable. However, reliability can be very expensive, so we should know how to manage it properly. 

Creating an overly-reliable system can be costly both in terms of money needed to achieve it, as well as in lack of time to focus on other important aspects of a product (e.g. new features). 

Since there are many factors that play into the reliability of a system, its almost impossible to measure them all, so we can decide to focus on unplanned downtime as a most encompassing risk our services face. With this in mind, two main parameters that we need to know in order to be able to manage service reliability are how available our services are ([[Measuring Service Availability]]) and what is our [[Service Availability Target]].

Since we never want (except for some extreme cases) to have 100% available system, we can manage the expected unreliability by utilizing [[Error Budgets]].


-----

Status: #💡 

References:
- [[Book - Site Reliability Engineering]] ([Source](https://sre.google/sre-book/table-of-contents/))
- [[Book - Designing Data Intensive Applications]] ([Source](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321))
