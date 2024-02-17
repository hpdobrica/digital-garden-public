---
title : Tracing
notetype : feed
date : 28-06-2022
---

Tracing is a type of [[Public/Monitoring]] which sacrifices the number of events it looks at to give us a picture of how a system behaves.

It's heavily relying on sampling - e.g. looking at only every hundredth request. Because of this, it can provide more context, and often records the stack trace together with how long each function took to execute.

It's a good way to find bottlenecks in applications and answer the question "which code paths cause the most latency?".

Distributed Tracing takes tracing a step further by attaching a unique trace id to a request, allowing you to stich together a path of a request across multiple services (tools like OpenZipkin and Jaeger)


-----

Status: #🌱 

References:
- 
