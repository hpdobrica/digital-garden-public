---
title : Monitoring
notetype : feed
date : 21-05-2022
---

When I was working as a developer on the first application that was actually running in production, we relied on looking at the application logs to figure out if something is wrong. We did it for a long time, and we were as proficient in it as one can get. 

I was routinely checking the logs for errors, when I noticed that something is off – in the postmortem, a smart man told me "logs should be the last place you should have to look when faced with an issue like this". This sentence seemed a bit absurd to me at the time – what do you mean, where am I supposed to look instead? Needless to say, back then, I knew nothing about monitoring.

Monitoring is an integral part of running services in production. Without it, we are blind to what's going on, and thus unable to act according to our best interest.

Providing visibility is in the center of monitoring, but speaking more broadly, monitoring allows us to:
- easily debug our systems
- see how a change impacts our system
- implement [[Alerting]] that something is broken or will break soon
- perform long-term trend analysis


When monitoring our system, we can look at what our user perceives which can show us currently active problems (e.g., high error rate, slow response times) – this is called **Black Box Monitoring**.

On the other hand, we can also look at internal metrics which are not directly visible to the user, which can give us insight into issues that are yet to come. For example, a user doesn't see that a disk is getting fuller, but they will get feel it once it's completely full. This is called **White Box Monitoring**.

To have an efficient monitoring system, it's very important to be able to tell what from why (what being 500 errors, why being database is refusing connections). 
This is best achieved with heavy use of white box monitoring with a bit of black box monitoring. 



Don't shy off from recording "the same metric" in different places – if you don't track both how slow your database server is, and how slow your application perceives it to be, you will not be able to tell a database issue from a network issue.




-----

Status: #💡 

References:
- [[{Site Reliability Engineering]]
