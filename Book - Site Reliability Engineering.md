---
title : Book - Site Reliability Engineering
notetype : unfeed
date : 22-11-2021
---

---

Source: [Site Reliability Engineering](https://sre.google/sre-book/table-of-contents/)

Status: #🛈/📖/♻️ 

---

### 1 - Introduction

- Apollo 8, understanding of system does not prevent human error  
- hope is not a strategy  
- important skills Unix system internals and l1-l3 networking  
- do work of ops, with skills of software engineers, automate everything  
- 50% ops work max, if more, find ways to circumvent (fallback to devs?)  
- challenges in hiring and requires management support to work out (stopping releases e.g.)  
- 100% availability is likely wrong target, 99.99% leaves us with 0.01% error budget  
- monitoring should be parsed by software, sent to a person only if they need to act, software should parse the alarm, not an engineer  
- valid monitoring output is either alerts, tickets or logging  
- more failures + less human intervention to fix them = more stable system  
- changes are biggest reason of failure so the rollout/detection/rollback procedure should be quick and automated  
- load testing and capacity planning  
- improving software efficiency improves capacity

### 2 - Infra at Google

- nothing too important, a lot of good references to research papers though

### 3 - Embracing Risk
- we want our services to be reliable but not too reliable, as more reliability costs in both resources needed to achieve it, as well as cost of opportunity (engineers could be working on new features instead)  
- there are too many types of risks for you to be able to affectively measure them all, so you can focus on unplanned downtime  
- this is the most straightforward way to measure availability (availability = uptime / (uptime + downtime))  
- in some cases (e.g. global systems), a better availability measurement is number of successful requests (availability = successful reqs / total reqs)  

- risk tolerance of service is different for infra and customer facing apps  
- for consumer services we can look at:  
	- target level of availability (depending on type of product, expected availability, what availability is offered for similar services etc.)  
	- what types of failures we get (sometimes we need to kill the app to stop data leak, sometimes we can schedule downtime when app is not used too much - is it better to fail a little all the time or totally fail at one moment?)  
	- cost (would we earn more if we had one more 9 availability? would additional earning cover the cost of running at one more nine?)  
	- other metrics like latency should also be considered  
- infra services are different in that they have different users with different goals (reliability for services vs throughput for offline processing)  
	- any of these cases can be handled by provisioning ultra reliable components, but that's too expensive - we should instead provide different tiers with different tradeoffs so that devs can make the decisions for themselves based on their needs  
  
- unreliability can be managed via error budgets  
- it's difficult for product teams and ops teams to find middle ground between investing in reliability and taking risks (too much testing and you are going too slow, reducing risk of deployments further or doing other work instead)  
- error budgets give us a way to determine this without guesswork and hope  
- product managers determine SLO from which we see how much time we should be available. The remaining time in the quarter is our error budget.  
- as long as uptime is above SLO, new releases can be pushed  
- now everyone knows their error budgets and can make risk tradeoffs accordingly

## 4 - Service Level Objectives

- in order to effectively measure availability of a service, we need to determine which metrics are important for it  
- we define SLA SLO and SLI to help us consider properties that matter to our service, determine action in case something goes wrong, as well as assure us that service is healthy  
  
- Service Level Indicators are quantitative measures of provided level of service  
	- common SLIs are latency, error rate, throughput, availability, durability of data  
	- measurements are often aggregated into rates, averages, percentiles  
	- sometimes we can't measure most important metrics (frontend latency) but we can measure the closest thing that we have available (backend latency)  
  
- Service Level Objectives are values or ranges in which SLIs are allowed to be  
	- for example, SLI is request latency, SLO is that it should be less than 100ms  
	- some SLOe might be forced upon us and some might affect others ( qps is dictated by user desires, qps directly affects latency)  
	- slo should drive our development decisions and set expectations for how service should perform (no more "service seems slow")
	- SLO should be reached but not overshot (promotes over-reliance, controlled chubby outage)  
  
- Service Level Agreements are formal or informal contracts between you and your users, which describes consequences of meeting or missing SLOs  
- if there are no consequences to breaking it, it's a SLO, otherwise it's SLA  
- SLA is business decision, not everything has SLA, but it should have SLI and SLOs  
  
- don't use every metric you have, use those that users care about  
- too much SLIs and you can't pay attention to everything, too little and you have holes in the examined behaviors of your application  

- indicator metrics can be collected on server side e.g. with [[Prometheus]], via periodic log analysis (how many 5XX responses?)
- in some cases server side indicators aren't good enough and a better metric would be a time to full page load (which could also catch bad js on frontend for example)

- when aggregating metrics, its much better to use percentiles than averages, as averages can often hide many things (most of the requests are completed in 50ms, but 5% are 20x slower, it would hardly be noticed on an average graph)
- you can standardize meanings of SLI definitions so that you don't have to repeat yourself everytime e.g.:
	- agreration intervals: "averaged over 1min"
	- aggretagion regions: "all tasks in the cluster"
	- how frequently are measurements made: "every 10 secs"
	- ...

- find out what users care about and find the closest thing you can measure
- its better to start from desired objectives and figure out the desired indicators 
- just measuring whats easy to measure gives you much more useless SLOs
- some tips for setting SLOs:
	- dont set targets based on current performance
	- SLIs should be kept simple (avoid complicated aggregations)
	- avoid absolutes (infinitely scalable, always available)
	- have as few SLOs as possible - if you cant prioritise something based on an SLO, it probably shouldn't be an SLO
	- better to start with loose target and tighten it as we go than to start with overly tight one
	- both overly aggressive and overly loose SLO can be damaging
- SLOs are a powerful way to set expectations for a service (knowing what to expect of a service will tell you whether its a good fit for your needs)
- dont over-achieve SLOs because users will grow to expect it as new standard (chubby)
- be more conservative on SLAs as they have penalties and are not as easy to modify as SLOs

## 5 - Eliminating Toil
- SRE teams need time to perform engineering tasks, so the operational work must be limited
- the kind of work SRE aims to reduce or eliminate is called Toil
- Toil is not just any "boring manual work"
- administrative tasks that have to be done and are not directly tied to running a production service (e.g. meetings, OKRs, paperwork) aren't toil, they are called Overhead
- toil is the work thats required for running services which tends to be manual, repetitive, automatable, reactive, not providing value and scales linearily with service
	- `manual` means either doing something completely manually, or manually running an automation script
	- `repetitive` means that if you are doing something for the first or second time, it can't be called toil. Toil is when you do something over and over again
	- `automatable` means that if a machine could perform the task as well as human could, it's probably toil. Human judgement required == not toil
	- `reactive` means that toil is work that appears as a reaction to various interrupts (e.g. firefighting, monitoring alarms), and is not strategy-driven
	- `not providing value` means that if the work has created any sort of permanent improvement to the system, it's likely not toil, however boring the actual task is
	- `scales linearily with service` means that as the service grows, the time dedicated to soliving this problem will grow approximately the same amount
- at google, SRE teams have a cap of 50% time spent on toil
- having less toil is better because:
	- it allows more time for engineering work
	- if left unhandled, toil has tendency to grow
	- if people work on toil too much their career tends to stagnate and morale of the team will fall
	- engineering work is what makes progress, so more toil means less progress
	- accepting toil shows to other teams that you are willing to do toil, possibly increasing the amount of toil in the future
- work done by SRE team can be divided into few sections:
	- engineering work
		- software engineering
		- systems engineering
	- toil
	- overhead
- every SRE should try to spend at least 50% time on engineering work
- if they can't something should change to allow them to
- some amount of toil is OK, but too much of it becomes really toxic

## 6 - Monitoring Distributed Systems
- this chapter offers guidance on what should be sent as an alert to the engineers, and how to deal with alerts that are less serious
- why have [[Monitoring]] on our systems?
	- long-term trend analysis
	- seeing how changes impact the system
	- alerting that something is broken or will break soon
	- having dashboards that show ?four golden signals?
	- help with debugging
- what to expect of monitoring/alerting
	- system should be able to automatically fix itself
	- if it cant fix itself it should notify an engineer
	- you should rarely alert just when something "seems a bit wierd"
	- every alarm is an interrupt, interrupts are expensive
	- we cant afford to have too much unnecessary noise on alerting
	- simple and fast is prefered for monitoring
	- avoid hiararchical dependencies (e.g. if db is slow alert for it, otherwise alert for slow website in general)
- its important to be able to tell what from why e.g. what is 500 errors, why is db refusing connections
	- do i care directly of this or is it useful where i debug?
- heavy use of white box monitoring with a bit of black box monitoring
	- white box = internal metrics, logs... (can show iminent problems, not yet visible to the user)
	- black box = monitoring exteranlly visible behavior (shows only active problems)
- its important to know both how slow database server is, and how slow a service percieves the database to be, otherwise you can't know a database problem from a network problem
- [[The Four Golden Signals of Monitoring]] are latency, traffic, errors and saturation
	- latency is the time taken to serve a request. distinguish between latency of failed and successful requests. separate the successful latency because errors can skew the image, but also track error latency to see how slow your error responses are
	- traffic shows how much demand is placed on the system. For web services it could be number of http requests. it can be broken down to request type (e.g. static content vs dynamic content requests). For a realtime service we could track network io rate and concurrent sessions
	- errors show a rate of failed requests either directly (500 error), indirectly (200 code but wrong response) or by policy (any request served over 1s is treated as error). 500 errors and LB level does a decent job of getting direct failed requests, only e2e tests can detect wrong content being served
	- saturation is how full your service is, with emphasis on the most constrained resource (e.g. if memory is our biggest constraint, we should show memory). note that performance often starts degrading before reaching 100% saturation, so it's important having utilization target to follow. Latency increases are often a leading indicator of high saturation, so it's good to suplement these with high-level latency metrics. Saturation is also caring about stuff like "your hard drive will be full in 4h"
- request latencies can be collected in buckets (e.g. number of requests served between 0 and 10 ms, between 10 and 30 ms, 30 and 100...) This is often a good easy way to see how your requests are distributed
- some measurements need bigger resolution (e.g. measuring cpu once a minute will hide short-lived spikes) and some don't need so big (e.g. no need to measure so often how full hard drive is)
- always aim for simplicity to avod creating a complex, fragile system that can't be changed
	- rules that catch incidents should be as simple and reliable as possible
	- data collection aggregation and collecting that's rarely exercised should be removed
	- signals that are collected but not exposed through dashboards or alerts should be removed
- ask following questions when building monitoring and alerting:
	- does this rule detect an otherwise undetected condition that is urgent, actionable and user visible?
	- will i ever be able to ignore this alert knowing its benign? how do i avoid this scenario?
	- does this alert mean that users are negatively affected? are there cases when they are not (e.g. drained traffic)? how can we exclude them?
	- can i take action in response to this alert? is it urgent or can it wait till morning? would the action be short term or long term fix? could it be automated?
	- are there multiple people getting paged for this issue?
- keep this in mind when setting up alarms:
	- every time pager goes off, i should be able to react with a sense of urgency
	- every alarm should be actionable
	- every alarm should require inteligence to respond to. if it doesn't, it should be automated
	- alarms should be about novel problems or events we haven't seen before
- its better for alarms to focus on symptoms rather than on causes
- at some points, extremely rare alarms might become frequent and require us to build a crude automation script to handle it. At this point we should either attempt to find the root cause and resolve it, or if root cause can't be found, fully automate the response
- there can often be tensions in the team over whether time should be spent on "hack solutions" in fear that they will lead to ignoring the real problem for indefinite amount of time. While it's a legitimate problem, the fear of this signifies mistrust in teams self discipline and ability to clean up tech debt. This is a big problem that needs to be escalated.
- dont look at every page separately - think of whether all the pages together lead to a healthy system and healthy team in the long run
- having a controlled, short term availability decrese for the long term availability increase is often a necessary trade-off for long-term stability of the system
- it's good to have a scheduled time (e.g. quarterly) to review number of incidents per on-call shift (taking that one incident might be composed of multiple alarms) 


## 7 - The Evolution of Automation at Google
- Automation is a powerful tool, but if done thoughtlessly, it can create as many problems as it solves
- manual operation < automated operation < autonomous system
- value of automation
	- if someone runs something many times, they run a risk of making a mistake - automation provides a solution to this in form of consistency
	- a good automation system can act as a platform that enables easier further automation, runs continuously, exports metrics about its performance
	- automation of fixes for common issues reduces mean time to repair (MTTR), reduces the time spent on fixing a problem and cleaning up after it and allows you to focus on other important stuff instead
	- automation can act faster than a human, and whenever it's possible, it should act instead of a human (automated procedures can make things worse, so this applies only to well-defined domains)
	- time saving is often the first automation value that comes to mind for many people. People often try to gauge whether the time required to automate a task would be worth it in terms of time saved (https://xkcd.com/1205/) - it's important to keep in mind that time saving here also comes from decoupling the operation from the operator - now anyone can easily and quickly execute this task without digging through documentation and complex handovers
	- "If we are engineering processes and solutions that are not automatable, we continue having to staff humans to maintain the system. If we have to staff humans to do the work, we are feeding the machines with the blood, sweat, and tears of human beings. Think _The Matrix_ with less special effects and more pissed off System Administrators."
- Value of automation for Google SRE
	- aim is to have everything expose an API, or to write their own api where public one is not available - first overcome the obstacles of automatic system management, and then work on the automation itself
	- create platforms wherever you can, or at least position yourself to be able to create platforms, as platform-based approach is necessary for manageability and scalability (?clarification of what this means?)
-  Use cases for automation
  - account creation
  - version upgrades
  - runtime config changes
  - fail over

- it's good to have external automation "glue logic", it's better to have software that doesn't need it at all
- automations outside of the system run a risk of becoming stale
- evolution of automation:
  - no automation
  - externally maintained system specific automation (script on someone's computer)
  - externally maintained generic automation (script is now part of a suite of scripts that everyone uses)
  - internally maintained system specific automation (system ships with its own script for automating the issue)
  - system that doesn't need automation 

- automate yourself out of a job
- the more time you save, the more time you have to automate other parts of the process, so the automation gains compound
- automation needs to be cautious of using implicit safety signals (e.g. if this file is missing it's safe to assume that disk is safe to wipe)
- python unit tests altered to look for cluster misconfigurations, and later extended with (idempotent) scripts to actually fix the misconfigurations automatically
- problem in above was that flaky tests might sometimes fail for no reason, and fix scripts could put the system in an inconsistent state
- automation processes can be evaluated in three respects: 
  - competence - how accurate they are
  - latency - how quickly they execute
  - relevance - how big part of a real world process is covered by automation
- making different people responsible for the service, and the automations tied to it, leads to different sorts of problems:
  - team taksed with speedy deployments has no incentive to fix technical debt of running the service in production
  - team not running the automation has no incentive to make the system easy to automate
  - management that doesn't care about automation will always prioritize new features
- better solution was to make service owners develop an admin server to handle cluster provisioning RPC requests. the teams provided both the automation code as well as apis that the automation needed
- highly effective automations have a downside of making human operators forget how to operate the system, so when automations fails, it becomes really hard or impossible to manually operate it
- in some cases, automation can be harmful to the system, but having the system scale makes automation non-optional
- automation is more useful than the simple time-invested/time-saved tradeoff
- in big systems, automation is required - in smaller systems, it's important to think of automation and build the systems with automation in mind


## 8 - Release Engineering

- release engineers as a role at Google
- teams should be self sufficient to allow scaling up
- release process is automated, and releases happen in small chunks to reduce differences between versions
- some projects push on green, others test a couple of versions and deploy the one that best passes the test
- builds must be hermetic and reproducible
- rebuilding old release for cherry pick should use the same build tools as the initial version used
- all code to main branch
- most projects don't deploy main branch directly, but split into a separate branch for releases and then never merge it back into main
- bug fixes always master first and then cherry pick into release branch (similar to gitlab flow?)
- investing into release engineering early on in the project is much cheaper than retrofitting the system for it later on

# 9 - Simplicity
