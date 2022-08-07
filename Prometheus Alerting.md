---
title : Prometheus Alerting
notetype : feed
date : 28-06-2022
---

Prometheus can create alert based on Alerting Rules. Alerting rules are another form of [[Prometheus Recording Rules]], which turn the results of the PromQL expressions into alerts that are sent to Alertmanager.

Alertmanager receives alerts from Prometheus and turns them into notifications (slack, email, pagerduty...) - note that **alerts are configured in prometheus, not in alertmanager**!

Alertmanager can aggregate related alerts, throttle alerts to reduce pager storms, mute alerts, and allows configuring different outputs for different teams. Its only job is sending a notification, human response should be managed by some other service or ticketing system.


-----

Status: #🌱  

References:
- [[Book - Prometheus Up And Running]]
