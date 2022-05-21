---
title : What should I Monitor
notetype : feed
date : 21-05-2022
---

When setting up [[Monitoring]] for a system that is able to output A LOT of metrics, it's often hard to determine which of these we should be monitoring.

If not sure where to start, covering [[The Four Golden Signals of Monitoring]] is typically a good place to start.

Some general tips:
- Don't shy off from recording "the same metric" in different places – if you don't track both how slow your database server is, and how slow your application perceives it to be, you will not be able to tell a database issue from a network issue.
- Collecting metrics like latency in buckets (e.g., 10-30ms, 30-100ms) is a good way to easily see that metric's distribution.
- Some metrics need higher resolution than others – when looking at a fast-changing metric like CPU usage, it's useful to have higher resolution, while things like hard disk fullness can be done with a much lower resolution.

-----

Status: #💡 

References:
- [[_Site Reliability Engineering]]
