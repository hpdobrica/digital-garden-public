---
title : Toil
notetype : feed
date : 21-01-2022
---

Toil is a type of work which is manual, repetitive, and brings no real long-term value to the project. In addition to this, toil is work that scales linearly with service, and can be solved by automation.

If some of these conditions are met, you are likely looking at toil. Any one of these on it's own does not signify that you are looking at work that's toil:
- `manual`  - either doing something completely manually, or manually running an automation script
- `repetitive` - if you are doing something for the first or second time, it can't be called toil. Toil is when you do something over and over again
- `automatable` - if a machine could perform the task as well as human could, it's probably toil. Human judgement required == not toil
- `reactive` - toil is work that appears as a reaction to various interrupts (e.g. firefighting, [[Monitoring]] alarms), and is not strategy-driven
- `not providing value` - if the work has created any sort of permanent improvement to the system, it's likely not toil, however boring and manual it might be
- `scales linearily with service` means that as the service grows, the time dedicated to soliving this problem will grow as well

Reducing the amount of toil is a big part of [[SRE]], as it helps the project in a few different ways:
- less toil leaves more time for engineering work ([[Types of work in SRE]])
- unhandled toil has a tendency to grow
- too much toil bring career stagnation and reduces the morale of the team


While we should always strive to reduce toil, it's important to note that some amount of toil is OK, but too much of it can quickly become toxic.


-----

Status: #💡 

References:
- [[~Site Reliability Engineering]]
