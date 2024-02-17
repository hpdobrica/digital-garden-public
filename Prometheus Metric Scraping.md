---
title : Prometheus Metric Scraping
notetype : feed
date : 28-06-2022
---

Once [[Prometheus Service Discovery]] gets us the list of targets to be monitored, [[Prometheus]] fetches the metrics by sending a "scrape" http request.

Once Prometheus receives a response to the scrape request, it parses the response, enriches it with details about scrape itself (e.g. was scrape successful, how long it took) and ingests it into storage. Scrape requests usually happen very often (e.g. every 10-60 seconds).

Based on this, we can see that Prometheus is a pull-based system, as the services only expose the metrics, while Prometheus itself reaches out to "pull" them. Trying to set up Prometheus in a push-based way is very ill advised.


-----

Status: #🌱 

References:
- [[Private/Book - Prometheus Up And Running]] ([Source](https://www.oreilly.com/library/view/prometheus-up/9781492034131/))
