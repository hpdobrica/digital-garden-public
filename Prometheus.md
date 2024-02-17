---
title : Prometheus
notetype : feed
date : 28-06-2022
---

Prometheus is an open source, metrics based [[Monitoring]] system. Its data model is kept as a time series, each consisting of key value pairs called labels.

PromQL is a querying language that allows for aggregation across any of these labels, allowing you to see metrics per process, machine, namespace, cluster. PromQL can be used to create graphs in software like Grafana and for creating alerts.

Prometheus works as follows:
- metrics are exposed by the application ([[Exposing Prometheus Metrics]])
- discovers scrape targets ([[Prometheus Service Discovery]])
- scrapes their metrics ([[Prometheus Metric Scraping]])
- stores their metrics ([[Prometheus Storage]])
- exposes these metrics to be queried or used to create alerts ([[Prometheus Querying]], [[Prometheus Alerting]])

It's also worth noting what Prometheus is not:
- not suitable for storing event logs or individual events
- not suitable for high cardinality data (e.g. emails and usernames)
- prometheus makes tradeoffs and prefers to give you 99.9% correct data then for your monitoring to break while looking for 100% correct answer. If high accuracy is needed, Prometheus should be used with caution



-----

Status: #🌱 

References:
- [[Book - Prometheus Up And Running]] ([Source](https://www.oreilly.com/library/view/prometheus-up/9781492034131/))
