---
title : Recreate Deployment Strategy
notetype : feed
date : 16-08-2022
---

Recreate [[Public/Deployment Strategy]] is a very simple strategy to set up. Here is how it works:
- you first terminate version `A`
- once that is done, you roll out version `B`

The advantage of this approach is that it's really simple to implement. The disadvantage is that it has high customer impact - the application is down from the moment version `A` is killed to the moment version `B` is successfully booted up.





-----

Status: #💡 

References:
- [Six Strategies for Application Deployment](https://thenewstack.io/deployment-strategies/)
