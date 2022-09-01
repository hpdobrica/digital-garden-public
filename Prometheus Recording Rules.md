---
title : Prometheus Recording Rules
notetype : feed
date : 28-06-2022
---

Recording rules allow us to evaluate and store results of PromQL queries in storage as a new time series, so we don't have to calculate everything on the fly whenever we want to render a graph. They are run on regular intervals to update the resulting time series.

This is especially useful for dashboards, as they re-compute all the queries every time they refresh.

-----

Status: #🌱 

References:
- [[Book - Prometheus Up And Running]] ([Source](https://www.oreilly.com/library/view/prometheus-up/9781492034131/))
