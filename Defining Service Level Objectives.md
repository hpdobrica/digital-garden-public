[]()---
title : Defining Service Level Objectives
notetype : feed
date : 09-01-2022
---

The first thing to know when choosing [[SLI]]s and [[SLO]]s is that [[SLO]]s should always be defined first. The thing we want to avoid by this is just picking whatever's easy to measure and ending up with useless objectives.

When defining SLOs, we should always start by asking "what do our users care about?". Once we have thought about it and have some ideas, we should find the closest thing that we can measure.

An example SLO definition might go something like `99% of GET requests (averaged over one minute) will be responded to in less than 100ms (measured across all backend services)`.

Here are a few things to keep in mind when defining your SLOs:
- the targets shouldn't be picked based on current performance - for example. if you are currently serving 99.999% requests successfully, this doesn't make it a good SLO to set as it doesn't leave any breathing space for future changes. Always reflect on the values before setting them, dont just use what's already there. That being said, when starting out, if you don't have enough data to base your decision on, taking current performance as a starting point and then iterating on it as you go would not be a bad idea
- [[SLI]]s that you measure should be kept simple - while it's possible to use complicated aggregations, they can hide the changes to system performance and are harder to reason about
- [[Avoid Absolute Statements]] - no SLO should specify that something is `infinitely scalable` or `always available`
- Have as few SLOs as possible - SLO should be able to carry its weight in a conversation. If SLO is breached and you can't get the development to prioritise fixing it just by mentioning the fact in the conversation, that thing is not worth having as a SLO
- its better to start with looser targets - you can always tighten the grip later
- note that setting too loose targets can lead to a bad product


Take note that some SLOs might be forced upon us, and some might be dependent on other SLOs - for example, we can't directly influence queries per second because this is based on user desires, but queries per second directly affect latency.

-----

Status: #💡 

References:
- [[Source - Site Reliability Engineering]]
