---
title : Service Availability Target
notetype : feed
date : 08-01-2022
---

When deciding the level of availability we want for our services, the target that we want to achieve is often described as a percentage of time the service is available.

This number is famous as a "number of nines". A system that's 99% available is said to have "two nines" service availability target, while 99.999% available system has "five nines".

The table below represents availability targets, together with how much downtime they allow per year/quarter/month/week/day:


| Availability 	| Year   	| Quarter 	| Month 	| Week  	| Day   	|
|--------------	|--------	|---------	|-------	|-------	|-------	|
| 90%          	| 36.5d  	| 9d      	| 3d    	| 16.8h 	| 2.4h  	|
| 95%          	| 18.25d 	| 4.5d    	| 1.5d  	| 8.4h  	| 1.2h  	|
| 99%          	| 3.65d  	| 21.6h   	| 7.2h  	| 1.68h 	| 14.4m 	|
| 99.5%        	| 1.83d  	| 10.8h   	| 3.6h  	| 50.4m 	| 7.20m 	|
| 99.9%        	| 8.76h  	| 2.16h   	| 43.2m 	| 10.1m 	| 1.44m 	|
| 9.95%        	| 4.38h  	| 1.08h   	| 21.6m 	| 5.04m 	| 43.2s 	|
| 99,99%       	| 52.6m  	| 12.96m  	| 4.32m 	| 60.5s 	| 8.64s 	|
| 99.999%      	| 5.26m  	| 1.3m    	| 25.9s 	| 6.05s 	| 0.87s 	|




-----

Status: #🌲 
References:
- [[Book - Site Reliability Engineering]]
- [Availability Table](https://sre.google/sre-book/availability-table/)
