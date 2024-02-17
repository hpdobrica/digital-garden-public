---
title : Blue Green Deployment Strategy
notetype : feed
date : 16-08-2022
---

Blue/Green is a [[Public/Deployment Strategy]] where version `B` is deployed alongside version `A`, after which the traffic is switched from `A` to `B`. 

## How it works
- before we start, we have 2 instances of `A` running and serving traffic 
- we deploy 2 instances of `B` alongside them, which are still not serving any traffic
- we confirm that version `B` deployment looks good
- we switch traffic flow from version `A` to version `B` on [[Load Balancer]] side

## Tradeoffs

Pros:
- zero downtime
- instant rollout and rollback
- entire application is changed in one go, no different api versions running at the same time

Cons:
- it expects us to run 2 identical environments alongside one another, which can be expensive
- it doesn't make much sense to run two databases, so you have to figure out how to run both versions connected to a single database (backwards-compatible db updates, decoupled db migrations from application deployment)


-----

Status: #💡 

References:
- [Six Strategies for Application Deployment](https://thenewstack.io/deployment-strategies/)
