---
title : Exposing Prometheus Metrics
notetype : feed
date : 28-06-2022
---

Depending on which software you are trying to expose [[Public/Prometheus]] metrics for, there are three options to achieve this.

### Pre-instrumented software

Many applications are already exposing metrics in Prometheus format. In case you are monitoring an application like this, you can just start using already existing metrics. Some examples are [[Public/Docker]] and [[Public/Kubernetes]].

### Client libraries

Prometheus client libraries allow for easy instrumentation of your own code. You add instrumentation code to your application to start exporting the metrics. This approach is known as **Direct Instrumentation**.

Since this code will be running alongside your application, it's important to understand how it will behave.

Metrics-based monitoring doesn't track individual events, so the number of events doesn't impact client memory usage. On the other hand, every new metric you track does add to the memory usage - keep this in mind when adding new metrics to your code!

If some code dependency (e.g. a http or rpc client) has instrumentation, it will be picked up by your application when you add the instrumentation code automatically. Instrumenting a common library allows all your services to expose the same metrics.

### Exporters

In case you are running code that isn't yours, client libraries will do you no good as you need to actually edit code to add them. Luckily, there is a good chance that this software already exposes some form of metrics that we could parse and hand off to Prometheus. 

An exporter is a piece of software running next to the application you want to instrument. Its task is to gather data from the application, and expose it to Prometheus in the correct format. This style of instrumentation is known as **Custom Collectors** or **ConstMetrics**.



-----

Status: #🌱 

References:
- [[Private/Book - Prometheus Up And Running]] ([Source](https://www.oreilly.com/library/view/prometheus-up/9781492034131/))
