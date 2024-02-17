---
title : Rolling Update Deployment Strategy
notetype : feed
date : 16-08-2022
---

Rolling Update is a [[Deployment Strategy]] (also known as Ramped or Incremental), where we slowly replace version `A` with version `B`. 

## How it works
- before we start, we have 2 instances of `A` running and serving traffic (let's call this `starting point` stage)
- until all instances of `A` are replaced with instances of `B` - repeat this:
	- a new instance of `B` is created, and once it's ready, it starts accepting traffic (`create new` stage)
	- once that happens, 1 instance of `A` is killed (`kill old` stage)

During this process, the number of instances over time changes like this:
- `A`: 2 `B`: 0 (`starting point` stage)
- `A`: 2 `B`: 1 (after `create new` stage)
- `A`: 1 `B`: 1 (after `kill old` stage)
- `A`: 1 `B`: 2 (after `create new` stage)
- `A`: 0 `B`: 2 (after `kill old` stage)


The example above replaces instances one at a time - we could configure this to be done with multiple instances in parallel.

During the deployment, our number of active instances is always between the desired count and (desired count + number of new instances rolling out at the same time).

## Tradeoffs

Pros:
- zero downtime
- pretty easy and cheap to execute

Cons:
- rollouts and rollbacks can last a long time (depending on number of instances and startup time)
- during deployment, some users will be served old version, some new version - we have no control over this aspect


-----

Status: #💡 

References:
- [Six Strategies for Application Deployment](https://thenewstack.io/deployment-strategies/)
