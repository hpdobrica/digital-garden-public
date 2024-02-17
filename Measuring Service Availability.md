---
title : Measuring Service Availability
notetype : feed
date : 08-01-2022
---

In order to know how available your service is, you need a way to measure it. One of the most straightforward ways to measure this is by measuring uptime:

```
availability = uptime / (uptime + downtime)
```

In some cases (e.g. global systems), a better availability measurement is the number of successful requests:

```
availability = successfull requests / total requests
```

It's also good to take other aspects of the system into consideration together with success rate. For example, instead of just looking at successful requests, you could look into successful requests that completed in less than two seconds. 

Measuring service availability is one of the most common [[SLI]]s.


-----

Status: #💡 

References:
- [[Private/Book - Site Reliability Engineering]] ([Source](https://sre.google/sre-book/table-of-contents/))
