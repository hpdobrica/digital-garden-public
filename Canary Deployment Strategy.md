---
title : Canary Deployment Strategy
notetype : feed
date : 16-08-2022
---

Canary is a [[Deployment Strategy]] where we gradually shift traffic from version `A` to version `B`. This is usually done via weighted load balancing (e.g., 90% traffic to `A`, 10% traffic to `B`).



## How it works
- before we start, we have 2 instances of `A` running and serving traffic 
- we deploy 2 instances of `B` alongside them, and send 10% of traffic to them
- we confirm that version `B` acts as expected while handilng 10% traffic
- we switch all traffic from version `A` to version `B`

## Tradeoffs

Pros:
- zero downtime
- testing new version on real traffic with a subset of random users, which allows us to monitor how new version behaves
- fast rollback

Cons:
- rollout speed is sacrificed for safety


-----

Status: #💡 

References:
- [Six Strategies for Application Deployment](https://thenewstack.io/deployment-strategies/)
