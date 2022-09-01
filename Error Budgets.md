---
title : Error Budgets
notetype : feed
date : 08-01-2022
---

It's difficult for product and ops teams to find middle ground between investing in reliability vs taking risks. If you test your software too much before releasing, you are going too slow and the market will swallow you, but if you don't test enough you will have a system which is not reliable enough to be used by clients.

Error budgets give us a way to make data-driven decisions on this spectrum without guesswork.

Here is how error budgets work:
- we define how much time we should be available in form of an [[SLO]]
- we do [[Measuring Service Availability]] to figure out how far we are from breaching our [[SLO]]
- the remaining time represents our error budget
- as long as there is more allowed downtime, new releases can be pushed
- if [[SLO]] is breached, only stuff which will improve our availability can be released

In a concrete example, having [[Service Availability Target]] of two nines allows us to have 21.6 hours of downtime per quarter. If we have been down for 10 hours this quarter already, this means that we have 11.6 hours of unavailability to spend during this quarter. Knowing this, we can make risk tradeoffs accordingly.



-----

Status: #💡 

References:
- [[[Book - Site Reliability Engineering]] ([Source](https://sre.google/sre-book/table-of-contents/))
- [Motivation for error budgets](https://sre.google/sre-book/embracing-risk/#xref_risk-management_unreliability-budgets)
