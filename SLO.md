---
title : SLO
notetype : feed
date : 09-01-2022
---

Service Level Objectives are values (or ranges of values) in which [[SLI]]s are allowed to be. For example, if [[SLI]] is request latency, SLO could be that request latency should be less than 100ms. 

SLOs are important in many ways in [[SRE]] philosophy, so it's important that [[Defining Service Level Objectives]] is done properly:
- they are a main component of [[Error Budgets]]
- they help drive our development decisions (should i work on new features or on improving latency?)
- they set the right reliability expectations (it's harder to be shocked by service being down if you know that it will be down 3.65 days every year ([[Service Availability Target]]), and helps developers using the service to take this into consideration)
- they help manage performance expectations - they put a stop to the "app seems slow" conversation. As you know exactly what slow means, there is no more guesswork


While meeting SLOs is important, over-achieving them is a bad idea, as people will adapt to it and take it as a new standard. If you have a flawless quarter, it might not be a bad idea to introduce a planned outage to come closer to the actual SLO.

-----

Status: #💡 

References:
- [[-Site Reliability Engineering]]
- [Service Level Objectives](https://sre.google/sre-book/service-level-objectives/)
- [Implementing SLOs](https://sre.google/workbook/implementing-slos/)
