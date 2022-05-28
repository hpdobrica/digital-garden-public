---
title : Video - Stop Talking & Listen; Practices for Creating Effective Customer SLOs
notetype : unfeed
date : 28-05-2022
---
---

Source: [InfoQ: Stop Talking & Listen; Practices for Creating Effective Customer SLOs](https://www.infoq.com/presentations/slo-pitfalls-2019/)

Status: #🛈/📹/✅ 

---


- sre workbook chapter 3 has case studies on implementing slos
- [[Cause Based Monitoring]]  / [[Symptom Based Monitoring]]
	- full disk, CPU usage  
	- you assume high CPU == slow service  
	- what if service is slow and CPU is fine?  
	- users don't care of CPU %  
	- full disk is another cause people don't care about, but they care about the symptom of not being able to access their data
	- They care about fast and reliable service instead, so we should differentiate between cause based and symptom based monitoring
	- it's easy to get caught up monitoring every possible signal to an issue
	- instead of correlating causes to experience, you can just measure the experience
	- causes are also useful, but are more useful to have during an outage than to signify an outage
- Customer pain is the biggest symptom
	- slos should be able to show availability levels so that, if barely met, most (typical) customers would be happy
	- meeting slo == happy customers / missing slo == sad customers
- getting data for our slos
	- defining critical user journeys (CUJ)
		- set of steps a user takes to accomplish some goal on your service
		- list all CUJs and order them by business impact
	- implementing SLIs - quantitative representation of some reliability aspect of your service (latency, correctness, availability)
		- sli = (good event / valid event) * 100
		- decide what ones would align with customer expectations
		- decide where to measure them
			- logs processing (allows backfilling, but no requests that didn't reach server)
			- app metrics (fast and cheap to add metrics, alo no requests that didn't reach)
			- infra metrics e.g. loadbalancer (easiest to get started, but cant measure more complicated requirements)
			- synthetic clients - probers that send requests regularly and validate the responses (can measure all steps of complex user journey, con is that you will have lots of probers and it starts to go into integration testing)
			- client instrumentation (most effective to measure user experience, but they also include stuff that is out of your scope e.g. poor network)
			- 
		- decide how to measure them
		- start with 1-3 SLIs per CUJ
		- e.g.:
			- if you have a store, most important part is when user shows intent to buy
			- availabillity would be measuring the proportion of successful requests - all of our interactions with this must be successful. it would look something like:
				- proportion of launched billing flows where server responds with successful status, measured by the game client and reported back asynchronously
			- for latency we want a proportion of valid requests served faster than a threshold
				- the proportion of /api/completePurchase requests with complete response served within 1000ms measured at the load balancer
	- finding coverage gaps
		- walk through your user journey and find coverage gaps, e.g. what happens if one step in there fails - probers could be used to check the correctness of this step
	- set SLOs
		- to decide on which target to use: 
			- look at past performance - if no one is yelling at you, your reliability target is probably ok for now
			- from here, try to be slightly above target and then later on start working on a more aspirational target
- common pitfals in setting SLOs
	- out of box metrics are good to get started, but youll need elbow grease
		- think about the tradeoffs on where to measure SLIs
		- readily available != good at portraying customer experience, you might need to put some work into this
		- always look at things for customer perspective, and invest effort into getting the best possible customer signal
	- over monitoring
		- less is more in monitoring
		- large amounts of variance and different sources make it harder to pinpoint issues
		- don't try to set up monitoring on every nook and cranny
		- make sure to periodicly clean up your monitoring data
		- instead of measuring all possible aspects of "browsing", e.g. searching, chosing categories, you can collect them all under just one metric which shows how browsing experience is looking to our customers
	- uptime != availability
		- distributed systems change the concept of availability as you can have 50 services up and 5 down
		- we don't care if we are just out, as long as there is no one using us anyway
		- it's better to think about it as a ratio of successful requests than of time spent up
		- collect requests on maintenance page to see how many you actually cant serve? many other ways to approach this as well
- iterating over our SLOs
	- my monitoring not screaming at me does not mean that everything is fine!- monitoring doesn't represent user experience, only users can be the judge of that
	- regular SLO reviews 
		- create feedback loops that you can do every 6-12 months to look at SLOs and try to make them better - we always want to make sure that they represent our users expectation with our service
		- in the beginning, you want to do this much more frequently
		- look at outage and support gaps
			- lets see how outage timespan was reflected on our monitoring
			- maybe use tags to show outages in monitoring directly?
			- use this as a chance to iterate on your SLOs
			- instead of outages, support tickets can also be valuable, but only if they are related to availability and performance
			- surveys and reaching out to customers is also a good addition, web trend analyzing as well
			- you can do all this proactively without being triggered by an outage
		- if there are no outages and everything is stellar, reviews might be used to loosen SLOs a bit and give engineers more breathing space
		