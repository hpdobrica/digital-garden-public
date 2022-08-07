---
title : Logging
notetype : feed
date : 28-06-2022
---

Logging is a form of [[Monitoring]] which looks at a limited set of events (e.g. all http requests, all db queries) and records part of their contexts

Logging sacrifices the amount of context provided for each event, but avoids sampling, so it's a perfect tool to investigate a particular request that went wrong.

Because logging doesn't sample and is triggered for every logged event, we need to make sure our logs are small enough - e.g. 1000 requests per second, 1000 bytes logged with each results in 84gb of logs per day!

Logging itself is a broad term which can be loosely divided into 4 categories: **Transaction Logs**, **Request Logs**, **Application Logs** and **Debug Logs**. 

It's important to make this distinction when implementing logging because not doing so will lead you into a position of having the volume of debug logs, with retention requirements of transaction logs.

#### Transaction Logs

These cover critical business records that need to be kept safe at all costs. Think anything money or compliance related, or touching any mission-critical features.

These are the logs that we want to keep almost forever, so there shouldn't be too many of them.

#### Request Logs

Logging things that happen as part of a single incoming request are request logs.

Applications may be able to process these logs to implement new features.

You don't want to lose request logs, but it wouldn't be the end of the world if some of them went missing. 


#### Application Logs

All logs produced by the operation of our application which are not tied to a request - think startup messages and maintenance tasks.

These logs should have a pretty low volume during normal operation - at most few logs per minute.

Application logs can be kept for some time to aid debugging, but are generally safe to get rid of one a certain time has passed.

#### Debug Logs

These are very detailed logs produced by the application on demand, which are expensive to store. Debug logs are threading the line between logging and [[Profiling]], and should be only enabled in specific debugging situations.

Ideally, we should have a "switch" to turn them on or off on demand.

Obviously, retention of debug logs should be very low - it would even be a good idea for them to never leave the physical machine they were created on.

-----

Status: #🌱 

References:
- 
