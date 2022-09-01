---
title : Measuring Traffic
notetype : feed
date : 29-05-2022
---

Traffic shows us how much demand is placed on the system, and is one of the [[The Four Golden Signals of Monitoring]].

How you track traffic, largely depends on what type of service you are running.

For web services, traffic can be represented as a number of HTTP requests. It might be useful to break the traffic measurements down by request type – for example, static content requests and dynamic content requests.

For a real-time service, we could track network IO rate and number of concurrent sessions.

For worker services, we could track the number of jobs injected into the system.

-----

Status: #💡 

References:
- [Site Reliability Engineering](https://sre.google/sre-book/table-of-contents/) ([[Book - Site Reliability Engineering|My Book Notes]])
