---
title : Consensus
notetype : feed
date : 13-12-2021
---

Consensus is an important concept in [[Distributed System]]s, which allows multiple servers to agree on some information.

In order for consensus algorithms to work, there are multiple rules which need to be followed by its members:
- if a process is to write a value, the write must be proposed by some other valid member
- all vald members must agree on the same value
- if all valid members agree on one value, any member has that value

There are two types of systems that use consensus depending on which members do what:
- in a symmetric system, any member can take in a request and process it, while the rest of the members will need to sync with that member about the request that just happened
- in an asymmetric system, only the elected leader does the request processing, while others sync to the leader

-----

Status: #🌱 

References:
