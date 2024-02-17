---
title : Prometheus Service Discovery
notetype : feed
date : 28-06-2022
---

Once your code is instrumented, [[Prometheus]] needs a way to find the services which are exposing the metrics. Yes, you could tell Prometheus where the services are and where they expose metrics, but this approach is not too scalable.

Prometheus has integrations with many service discovery mechanisms ([[Kubernetes]], AWS EC2, Consul). There is also a generic integration for people who are using some more custom solution.

With each integration, you can configure the rules by which Prometheus will scrape your service discovery system (e.g. look for a specific label on the pods). You can also use relabeling to configure how the metadata from your service discovery system maps to resulting Prometheus metrics.


-----

Status: #🌱 

References:
- [[Book - Prometheus Up And Running]] ([Source](https://www.oreilly.com/library/view/prometheus-up/9781492034131/))
