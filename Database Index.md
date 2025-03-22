---
title : Database Index
notetype : feed
date : 15-03-2025
---

[[Database]] indexes are data structures that databases keep on the side to improve the speed of reading the primary data, at the cost of increased storage usage and speed of writes.

Indexes are derived from the primary data, and in many databases you can safely add and remove the without affecting the original data - just the speed of query execution.

Indexes optimize the speed of read queries, usually at the cost of speed of write queries. It's difficult to use a secondary data structure to improve write speeds, as the fastest way to write something is to write it only once - while indexes are active, in addition to writing the data to the database, you also need to update the indexes, which slows the writes down.

Some index types:
- [[In Memory Hash Map Index]]

-----

Status: #📥

References:
-  [[Book - Designing Data Intensive Applications]] ([Source](https://www.amazon.com/Designing-Data-Intensive-Applications-Reliable-Maintainable/dp/1449373321))
